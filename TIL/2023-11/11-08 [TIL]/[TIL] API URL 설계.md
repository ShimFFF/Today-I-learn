# [TIL] API URL 설계

### 목차
- [\[TIL\] API URL 설계](#til-api-url-설계)
    - [목차](#목차)
  - [😃 잡담](#-잡담)
  - [📄 배운 내용](#-배운-내용)
    - [API 설계 시 필요한 것](#api-설계-시-필요한-것)
  - [API Endpoint](#api-endpoint)
    - [HTTP 메소드](#http-메소드)
    - [URL](#url)
    - [💡 RESTful한 API의 Endpoint 규칙](#-restful한-api의-endpoint-규칙)
  - [세부적 API 설계](#세부적-api-설계)
    - [Path variable](#path-variable)
    - [Query String](#query-string)
    - [Request  Body](#request--body)
    - [Request Header](#request-header)

##  😃 잡담
오늘은 서버 스터디를 위해 API 설계에 대해 공부 했다.<br>
공부 하며 내가 실제로 프로젝트를 하며 봤던 API 명세서에 대해 더 잘 이해할 수 있었다. 사실 그때는 몸통 박치기 식으로 프로젝트를 했던 때라, 하나 하나 찾아가며 이해하며 플젝을 하기 보다는 주어진 Task를 기한안에 완료하는 것을 목표로 두었다. 그렇게 프로젝트를 하며 API 문서에 적힌 것들이 의미하는 바에 대해 궁금했었는데, 지금 공부하게 되었다.!  <br>
공부하며 지금 진행하고 있는 묘집사 플젝의 API 명세서도 다시 살펴봤다. 우리 팀 서버 분들은 어떤 식으로 설계를 했는지 알 수 있었다. 하지만 하직까지 어떤 식으로 API를 설계하는 것이 좋은 것인가? 라는 것에 대해서는 확실하게 감이 잡히지는 않는다. 서버 파트로 플젝을 진행하기 전에 관련 자료들을 찾아보고 TIL이나, 벨로그에 정리해야겠다.


## 📄 배운 내용
### API 설계 시 필요한 것

1. **API End Point 설계**
2. **요청 데이터, 응답 데이터의 설계**

*→ 위 정보를 문서화 한 것이 **API 명세서***

**REST API** : HTTP 메소드와 자원을 이용해 서로 간의 통신을 주고 받는 방법

## API Endpoint

REST API에서의 endpoint

### HTTP 메소드

> REST 방식으로 통신 할 때 필요한 작업을 표시하는 방법
> 

| GET | 조회 |
| --- | --- |
| POST | 생성 (정보를 넘기고 처리를 요청) |
| PUT | 갱신 (전체) |
| PATCH | 갱신 (일부) |
| DELETE | 삭제 |

### URL

### 💡 RESTful한 API의 Endpoint 규칙

- URL에 동사가 포함되면 안됨
- URL에 단어의 구분이 필요한 경우 -(하이픈)을 사용
- 자원을 기본적으로 복수형으로 표현
- 하나의 자원을 명시적으로 표현하기 위해서는 `/user/id` 처럼 식별 값을 추가로 사용
- 자원 간 연관 관계가 있을 경우 이를 URL에 표현

<br>

- ***로그인, 회원 가입, 탈퇴 예시***
    - 도메인 주소가 `https://hana.com` 인 경우
    
    - **로그인**<br>
      💡 ***`POST https://hana.com/users/login`***
        
        
    
    - **회원 가입**<br>
        💡 ***`POST https://hana.com/users`***
  
        - POST /users/id의 형태로 설계를 못함
            - 회원 가입 전이므로 유저를 식별할 값이 없음
            
    - **회원 탈퇴**<br>
        💡 ***`PATCH https://hana.com/users`***
        
        - 비활성 계정으로 만들고,추후 계정 복구를 고려하여 PATCH로 설계

<br>
        
- ***리소스 간 연관 관계가 있는 경우의 예시***
    
    
    교사가 여러 개의 교과목을 강의할 수 있고, 교사와 교과목이 1:N인 경우
    
    - **교과목의 목록을 조회**<br>
        💡 **`/users/subjects`**
        
    
    일단 사용자는 교사만 있다고 가정
    
    - **특정 교사의 교과목 목록을 조회**<br>
    💡 **`/users/id/subjects`**
        1. 교사가 여러 개의 과목을 강의
        2. 계층 관계는 교사 다음 교과목
        3. URI상에 교사가 더 계층 관계 상 우선이 된다는 것을 표현
    
<br>

- ***N:M 관계의 예시***
    
    **게시글과 해시태그의 경우**
    
    `/articles/hash-tag`, `/hash-tag/articles` 중에 어떻게 설계해야할지
    - 💡  **비즈니스 로직상 더 중요한 대상을 계층 관계에서 앞에 두기**
    
    **`/articles/hash-tag`**
    
    <br>

## 세부적 API 설계
1.  **path variable *(endpoint에 포함)***
2. **query string**
3. **request body**
4. **request header**

### Path variable

> 단 하나의 특정 대상을 지목할 때 활용
> 

**특정 교사의 교과목 목록을 조회**


💡 **`/users/id/subjects`**



해당 예제에서 각 강사의 고유 아이디 값을 넣어야 함

**→ id는 ‘id’가 아닌 식별값을 의미함**


💡 **`/users/{user-id}/subjects`**

*단어 구분은 `-`(하이픈)을 사용하여 함*


<br>

### Query String

> 특정 여러 개 값을 조회할 때
> 

**→ 보통 검색 조회에 많이 활용**

***글 이름에 hana가 포함된 게시글을 조회**


💡 `GET /users/articles**?name=hana`**



**글 이름에 hana와 umc가 포함된 게시글을 조회**


💡 GET /users/articles**?name=hana&club=umc**


→ `&`을 통해 연결

> **쿼리 스트링은 API 엔드 포인트에 포함되지 않음**
> 
> 
> 따라서 엔드포인트는 **`GET /users/articles`** 임 

<br> 

### Request  Body

1. POST로 서버로 데이터를 넘겨주는 경우
2. 어떻게 데이터를 넘길 것인가?
3. 데이터 그 자체를 URL에 노출하는 것은 위험

<br>

💡 **request body에 해당 데이터를 담기!**

→ **json의 형태** 혹은 **form-data 형태**


**이름 , 전화번호, 닉네임의 정보가 필요한 경우 json의 형식**

```sql
{
	“name” : “심세원”,
	“phoneNum” : “010-1111-2222”,
	"nickName" : "hana",
}
```

<br>

### Request Header

> 전송과 관련된 기타 정보들이 담기는 부분
> 

ex)  json인지, 아니면 form-data인지 담기

대표적으로 토큰을 헤더에 담아 로그인 됨을 알려줌