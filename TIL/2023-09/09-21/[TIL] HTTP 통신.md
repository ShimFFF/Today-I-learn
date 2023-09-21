# TIL : [ Network / HTTP 통신 ]

> Velog - [[Network]-HTTP 통신 쉽게 이해하기](https://velog.io/@ssw123/Network-HTTP-%ED%86%B5%EC%8B%A0-%EC%89%BD%EA%B2%8C-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0#2-%ED%97%A4%EB%8D%94-%EB%91%90-%EB%B2%88%EC%A7%B8-%EC%A4%84%EB%B6%80%ED%84%B0)

##  😃 잡담
오늘은 간단하게 HTTP 통신에 대해 정리해봤다.

정리하면서 2023 상반기에 진행한 안드로이드 스터디가 생각났다. 해당 스터디를 진행하며 안드로이드에서의 HTTP 통신에 대해 공부하며 간단하게 HTTP 통신에 대해 정리했었는데, 네트워크에 대해 공부하고 있는 지금 다시 더 자세히 정리해봤다. 정리 하면서 스터디 때 했던 내용이 생각나기도 했고 이제는 누가 물어보면 쉽게 설명해줄 수 있다!

안드로이드에서는 보통 API를 연결할 때, retrofit2를 사용해서 HTTP 통신을 구현하는데, 나는 보통 `retrofitManager`, `retrofitInterface`, `retrofitCilent`, `Response`, `Request`로 나눠서 구현한다. 이런 구현 방법도 나중에 정리해서 벨로그에 올려야겠다.

## 📄 공부한 내용
### HTTP
> 텍스트 기반의 통신 규약으로 인터넷에서 데이터를 주고받을 수 있는 프로토콜

**Request :**<br>
클라이언트가 서버에게 보내는 요청 메시지

**Response :**<br>
서버가 클라이언트에게 보내는 응답 메시지

### 특징
**상태를 유지하지 않는 프로토콜**
- 따라서, 정보 저장에 쿠키, 세션을 사용
- 따라서, 요청/응답 방식으로 동작

<br>

**TCP/ IP를 이용하는 응용 프로토콜**

  **TCP:** 
  > 데이터의 전송을 제어하는 프로토콜

  **IP:** 
  > 인터넷 프로토콜

  <br>

  ### HTTP Protocol의 주요 Method(동작)

| GET | 서버로부터 리소스(데이터)를 요청 |
| --- | --- |
| POST | 서버에 새로운 데이터를 전송 or 리소스를 생성 |
| PUT | 서버에 데이터를 업데이트하거나 리소스를 생성 or 교체 |
| DELETE | 서버에서 데이터를 삭제 |
| PATCH | 서버의 데이터 일부를 수정 |

<br>

### HTTP의 데이터를 주고 받는 형식 3가지
1. **From-data** 

2. **JSON (JavaScript Object Notation)**

3. **XML (eXtensible Markup Language)**
   
   <br>

## ✨ 앞으로의 계획
- retrofit2를 이용한 안드로이드에서의 HTTP 통신 정리하기
  - 이렇게 정리해서 아카이빙 해두면 나중에 내가 찾아보기도 좋다..! ㅎㅎ
- Application Layer 공부하기