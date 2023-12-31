# TIL : [Algorithm / Memorization Algorithm과 잡담]

> Velog - [[알고리즘] Memoization Algorithm](https://velog.io/@ssw123/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Memoization-Algorithm)

### 잡담
오늘은 LCS에 대해 공부하려다가 그 기본이 되는 Memoization Algorithm에 대해 먼저 정리를 진행했다. 

솔직히.. 정리를 한 후에 LCS까지 정리를 진행하고 싶었지만, 졸업한 고등학교에서 진행하는 인터뷰를 준비하느라 꽤 긴 시간이 흘러버려 Memoization Algorithm까지만 정리 했다. 해당 인터뷰가 다른 고등학교 선생님들을 위해 강당에서 진행되는 만큼 준비에 공을 들이느라 고등학교 시절을 돌아볼 수 있었는데, 고등학교 시절에 더 많은 도전을 했었더라면 어땠을까 하는 아쉬움이 남았다. 그런 만큼 지금 현재는 도전적인 태도로 많은 경험을 해야겠다는 생각 또한 할 수 있었다. 또한 고등학교 시절 친구들과 다양한 문제와 토픽에 대해 논의 했던 것이 생각났는데, 해당 경험으로 특정 토픽에 대해 고차원적으로 이해할 수 있었다. 그때를 떠올리며 더 많은 궁금증과 질문을 하며 이쪽 분야에 대해 이해를 올려가야겠다. 조만간 개발자가 질문하는 법도 배워야겠다. 할튼 잡담은 여기서 끝내고 오늘 공부한 것에 간단히 정리하자!

## 📄 공부한 내용
### Memoization Algorithm
>프로그램이 동일한 계산을 반복적으로 해야 할 때, 이전에 계산한 값을 메모리에 저장하여 중복적인 계산을 제거하여 전체적인 실행 속도를 빠르게 해주는 기법

<br>

**특징**
- 동일한 계산 반복 제거
- 이전 결과 저장
- 전체 실행 속도 향상
  
<br>

해당 내용의 가장 대표적인 예시로는 **피보나치 수열**이 있다.

> Memoization Algorithm을 사용하면 중복 계산을 피할 수 있다는 것이 피보나치 수열을 보면 가장 직관적으로 보인다.

<br>

보통 **Memoization Algorithm**은 큰 문제를 해결하기 위해 작은 부분 문제를 반복적으로 해결하는 경우에 사용한다

나는 이 말을 나름대로 표현했는데 **n번째의 solution이 n-1, n-2의 solution**을 포함하고 있을 때 사용한다고 표현했다.

## ✨ 앞으로의 계획
- LCS에 대해서도 정리하고 Memoization Algorithm을 활용해서 푼 문제도 깃에 올려야겠다.
- 개발자가 질문하는 법에 대해 배우자
  - 잘 답변하는 법도!
-  알고리즘과 데이터 구조에 대해 지속적으로 공부하고 실력을 향상시켜야겠다.
   - 이러한 개념을 이해하고 활용하면 문제 해결 능력이 향상되며, 더 효율적이고 최적화된 소프트웨어를 개발하는 데 도움된다.
  