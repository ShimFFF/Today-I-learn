# [TIL] Spring 3.x 버전에 Redis 설정하기

## 📄 배운 내용

로그인을 완료하면, 유효기간이 짧은 Access Token과 유효기간이 긴 Refresh Token을 발급해줌
-> 우리 프로젝트에서는 Refresh Token을 Redis에 저장하기로 했다.
-> 아직 로그인 로직 개발 전이니, 내가 할 것은 Redis 연결, 예제 Service 구현, Test 진행 정도?

### 동작 방식
1. 유저가 로그인하면, 서버에서 access token과 refresh token을 발급
2. 서버는 refresh token을 저장
3. 유저는 access token과 refresh token을 안전한 저장소에 보관
4. 유저는 인증이 필요한 작업을 할 때, refresh token을 서버에게 보냄
5. 서버는 access token의 유효성을 검증한 뒤 작업을 허용
6. access token이 만료되었다면, access token이 만료되었다는 응답이 줌
7. 유저는 refresh token을 서버에게 보냄
8. 서버는 refresh token의 유효성을 검증
9. DB에 저장된 refresh token과 동일하다면, access token qkfrmq
10. 유효하지 않거나 동일하지 않으면 refresh token 삭제 (다시 로그인 하도록 함)


## 구현 과정
### 1. Redis 설치
- [Redis 설치](https://redis.io/download)

### 2. Redis 연결
**redis dependency 추가**
```gradle
implementation 'org.springframework.boot:spring-boot-starter-data-redis'
```

**application.yml 추가**
```yaml
spring:
  data:
    redis: # Redis 설정
      host: localhost # Redis 서버 주소 (배포서버의 경우 localhost가 아닌 ec2 주소를 사용)
      port: 6379
```

**RedisConfig.java 추가**
```java
@Configuration
public class RedisConfig {

    @Value("${spring.data.redis.host}")
    private String host;
    @Value("${spring.data.redis.port}")
    private int port;

    @Bean
    public RedisConnectionFactory redisConnectionFactory() {
        return new LettuceConnectionFactory(host, port);
    }

    @Bean
    public RedisTemplate<String, Object> redisTemplate(RedisConnectionFactory redisConnectionFactory) {
        RedisTemplate<String, Object> template = new RedisTemplate<>();
        template.setConnectionFactory(redisConnectionFactory);
        template.setKeySerializer(new StringRedisSerializer());
        // Set other serializers if needed
        return template;
    }
}

```

### 3. 예제 Service 구현
**RefreshToken entity 구현**
- 따로 id를 생성하지 않고, memberId를 id로 사용
```java
@AllArgsConstructor
@Getter
@Builder
@RedisHash(value = "jwtToken", timeToLive = 60*60*24*30) // 30일
public class RefreshToken { //redis에 저장할 객체

    @Id
    @Indexed // 인덱스를 걸어주면 조회할 때 빠르게 찾을 수 있음
    private UUID memberId;

    private String refreshToken;

    /*
    만료된 access Token을 가진 memberId 값으로  refresh Token을 찾아와서 유효성을 검사할 예정
     */
}
```

**RefreshTokenService.java**
```java

@Service
@RequiredArgsConstructor
public class RefreshTokenService {

        private final RefreshTokenRepository refreshTokenRepository; // Redis에 저장된 refreshToken을 가져오기 위해 DI

        @Transactional
        public RefreshToken saveTokenInfo(String refreshToken, UUID memberId) { // Redis에 refreshToken 저장
            return refreshTokenRepository.save(
                    RefreshToken.builder()
                            .memberId(memberId)
                            .refreshToken(refreshToken)
                            .build()
            );
        }

        @Transactional
        public RefreshToken findByMemberId(UUID memberId) { // 만료된 accessToken으로 refreshToken을 찾아옴
            return refreshTokenRepository.findByMemberId(memberId).orElseThrow(() -> new IllegalArgumentException("Refresh Token이 존재하지 않습니다."));
        }

        @Transactional
        public void delete(RefreshToken refreshToken) { // Redis에 저장된 refreshToken 삭제
            // Redis에 저장된 refreshToken 삭제
            refreshTokenRepository.delete(refreshToken);
        }
}
```

### 4. Test 진행
**RefreshTokenServiceIntegrationTest.java**
```java

@SpringBootTest
public class RefreshTokenServiceIntegrationTest {

    @Autowired
    private RefreshTokenService refreshTokenService;


    @Test
    void testSaveTokenInfo() {

        final String REFRESHTOKEN = "testSaveTokenInfo";
        final UUID MEMBERID = UUID.randomUUID();


        // When
        RefreshToken savedToken = refreshTokenService.saveTokenInfo(REFRESHTOKEN, MEMBERID);

        // Then (test에서 사용되는 assertion, 조건이 참이 아니라면 테스트 실패)
        assertNotNull(savedToken);
        assertEquals(REFRESHTOKEN, savedToken.getRefreshToken());
        assertEquals(MEMBERID, savedToken.getMemberId());
    }

    @Test
    void testFindByAccessToken() {

        final String REFRESHTOKEN = "testFindByAccessToken";
        final UUID MEMBERID = UUID.randomUUID();

        RefreshToken savedToken = refreshTokenService.saveTokenInfo(REFRESHTOKEN, MEMBERID);

        // When
        RefreshToken foundToken = refreshTokenService.findByMemberId(MEMBERID);

        // Then (test에서 사용되는 assertion, 조건이 참이 아니라면 테스트 실패)
        assertNotNull(foundToken);
        assertEquals(REFRESHTOKEN, foundToken.getRefreshToken());
        assertEquals(MEMBERID, foundToken.getMemberId());

    }

    @Test
    void testDeleteByAccessToken() {

        final String REFRESHTOKEN = "testDeleteByAccessToken";
        final UUID MEMBERID = UUID.randomUUID();

        RefreshToken savedToken = refreshTokenService.saveTokenInfo(REFRESHTOKEN, MEMBERID);

        RefreshToken tokenToDelete = refreshTokenService.findByMemberId(MEMBERID);

        // When
        refreshTokenService.delete(tokenToDelete);

        // Then (test에서 사용되는 assertion, 조건이 참이 아니라면 테스트 실패)
        assertThrows(IllegalArgumentException.class, () -> refreshTokenService.findByMemberId(MEMBERID));

    }
}
```