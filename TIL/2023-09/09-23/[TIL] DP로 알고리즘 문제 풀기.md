# [TIL] : DP로 알고리즘 문제 풀기

> Velog - [[알고리즘]-Dynamic Programing(DP)를 활용해 Distinct Subsequences 문제 풀기](https://velog.io/@ssw123/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Dynamic-ProgramingDP%EB%A5%BC-%ED%99%9C%EC%9A%A9%ED%95%B4-Distinct-Subsequences-%EB%AC%B8%EC%A0%9C-%ED%92%80%EA%B8%B0#%EC%9E%90%EC%84%B8%ED%9E%88-%EC%84%A4%EB%AA%85)

##  😃 잡담
오늘은 Dynamic Programing과 Memoization을 이용한 알고리즘을 풀었다. 

사실 동적 계획법을 이용하지 많고 문제를 풀어볼려다.. 많은 시간을 보내고 문제도 풀지 못해서 결국 동적계획법을 이용해 문제를 풀었는데, 역시 사람들이 미리 만들어 놓은 방법을 쓰니까 훨씬 쉽고 빨리 문제를 풀었다.

검색, 누군가의 도움 없이 알고리즘 문제를 푸느라 시간이 생각보다 꽤 걸리긴 했는데 그래도 풀고 나니까 성취감도 느껴지고 Dynamic Programing과 Memoization에 대해 조금은 더 알 것 같다.

주석도 열심히 달아서 알고리즘 문제 저장하는 레포에도 올렸다
> Github - [Algorithm/code/Distinct Subsequences](https://github.com/ShimFFF/Algorithm/tree/main/code/Distinct%20Subsequences)

역시 알고리즘 푸는 건, 처음 시작할 때는 살짝 막막하지만 어떻게 풀지 집중해서 생각하고 코드를 작성하다 보면 집중도 잘되고 재미있는 것 같다.. (아직까지는 ㅎㅎ) 이번 하반기에는 알고리즘 공부를 하고 있는데, 하는 김에 열심히 해봐야겠다.!

그리고 요즘 TIL을 쓰면서, Velog에 글도 꽤 쓰고 있는데 나중에 한번 개발자가 블로그 글 쓰는 법 같은 것도 찾아서 좀 더 좋은 글을 쓸 수 있도록 해야겠다.!

<br>

## 📄 공부한 내용
오늘은 공부한 내용이라기 보다는 DP를 사용해 문제를 풀어간 과정을 기록하겠다!

### 문제
**Distinct Subsequences**<br>
어떤 Sequence에서 특정 Subsequence가 서로 다른 인덱스 순서로 몇 번 등장하는지를 세기

**INPUT**<br>
문자열 X (Sequence)<br>
문자열 Z (Subsequence)


**OUTPUT**<br>
문자열 X에서 문자열 Z가 서로 다른 인덱스 순서로 등장하는 서로 다른 서브시퀀스의 수

### 풀이
1. dp[0][i], dp[j][0]을 0으로 초기화 해줌
   
2. 문자열 X를 순회하면서 문자열 Z의 첫 번째 문자와 일치하는 문자를 찾음
   
3. 일치하면 +1 값을 해서 할당. (끝까지 해줌 dp[j][1]++;) (일치하지 않으면 dp[j][1]=dp[j-1][1])
   
4. 그 후 dp 값을 모두 채워감.
   
5. 일치하는 문자를 찾으면, dp[j][i]=dp[j-1][i]+dp[j][i-1] 의 값을 할당 (일치하지 않으면 dp[j][1]=dp[j-1][1])
   
6. dp[x'][z']의 값이 서로 다른 인덱스 순서로 등장하는 서로 다른 서브시퀀스의 수
(x'=X의 길이 z'=Z의 길이)

<br>

해당 과정을 진행하면 배열이 다음과 같이 채워진다.
```
0 0 b a n a n a
0 0 0 0 0 0 0 0
a 0 0 1 1 2 2 3
n 0 0 0 1 1 3 3
a 0 0 0 0 1 1 4
```

<br>

## ✨ 앞으로의 계획
- 알고리즘 공부하기
- 블로그 글쓰는 법 찾아보기