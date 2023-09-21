# TIL : [DB / SQL Parsing]

> Git 정리본 - [Database System Concept 7th Problem Solving Chapter 1](https://github.com/Poin-Book/2023.09-database/blob/main/Chapter%2001%20-%20Database%20Introduction/Appendix_A%20-%20%EA%B3%BC%EC%A0%9C%20%ED%92%80%EC%9D%B4/Note.md)

학기를 시작하며 데이터베이스와 네트워크 스터디를 하고 있다.
오늘은 SQL과 같은 선언적 쿼리 언어를 사용하는 이유에 대해 이야기를 나누며, 나는 최적화와 최적 실행 계획 때문에 사용한다고 설명했다. 스터디원 중 한명이 이에 대해 더 이해하고 싶다면 쿼리 파싱을 찾아보면 된다고 했다. 이에 쿼리 파싱에 대한 내용을 찾아봤고 여기에 간단히 정리하고자 한다.

## 📄 공부한 내용

### SQL의 과정

- **SQL 파싱**<br>SQL 쿼리를 컴퓨터가 이해하고 처리할 수 있는 내부 구조로 변환하는 프로세스
  - **SQL 문장의 구문 분석(Syntax Parsing)**: <br>SQL 문장의 문법을 검사하고 쿼리 문장의 토큰화(tokenization)를 수행하여 SQL 문장의 구조를 파악
  - **SQL 문장의 의미 분석(Semantic Parsing)**: <br>SQL 문장의 의미와 의도를 이해하고 데이터베이스 스키마와 연관시켜 어떤 작업을 수행할지 결정

- **쿼리 최적화**<br>SQL 쿼리를 효율적으로 실행하기 위해 최적 실행 계획을 수립. 이 단계에서 데이터베이스 시스템은 다양한 실행 계획을 비교하고 가장 효율적인 방법을 선택

- **실행 계획 생성**<br>최적 실행 계획을 바탕으로 데이터베이스 시스템이 실제로 데이터를 검색하고 조작하기 위한 실행 계획을 생성

<br>

### 쿼리 최적화
쿼리의 실행 속도를 최적화하기 위한 프로세스로 **DB 시스템이 여러 실행 계획을 고려하고 가장 효율적인 실행 계획을 선택해 쿼리를 실행함** <br>
-> 말 그대로 "최적화"를 목표로 하는 단계

쿼리를 파싱하여 트리 형태로 만들고 이를 논리적, 물리적 최적화 과정을 수행

<br>

***Optimizer*** : 프로시저를 만들어내는 DBMS 내부 엔진
주어진 SQL 쿼리를 가장 효율적으로 실행할 수 있는 방법을 결정
  
1. SQL 쿼리를 분석하고 테이블, 인덱스, 통계 정보 등을 고려하여 최적 실행 계획을 수립

2. 최적화된 실행 계획을 통해 데이터베이스에서 데이터를 검색하거나 조작

## ✨ 앞으로의 계획
- 데이터베이스와 네트워크 스터디를 계속 진행하면서 내용에 대해 더 깊은 이해를 하고 지식을 공유할 예정이다.
- 쿼리 최적화에서 중요한 주제인 타입 추론, 비용 계산, 조인 순서, 필터링 위치 결정에 대해서도 학습하고 이해를 높일 것이다.
- 현재 Spring에 대한 스터디와 개발이 예정되어 있는 만큼 DB에 대한 학습을 지속하겠다.
- 스터디를 통해 공부하고 지식을 공유하는 경험이 유익하다는 것을 느껴, 나중에 기회가 되면 직접 스터디를 주최하고 진행해보고 싶다.