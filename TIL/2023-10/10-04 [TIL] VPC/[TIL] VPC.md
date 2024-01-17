# [TIL] VPC
>[velog] - [[네트워크]-AWS의 VPC에 대해](https://velog.io/@ssw123/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-AWS%EC%9D%98-VPC%EC%97%90-%EB%8C%80%ED%95%B4)

##  😃 잡담
AWS에 대해서 잘 알지 몰랐기에 VPC 정리에 대해 좀 공을 들였다. VPC를 제대로 이해하려면 서브네팅, LAN, 사설 IP 등 cs 지식에 대해서도 알아야 했는데, 이런 것들도 하나 하나 다 찾아가면서 했다.<br>
개념을 하나 하나 이해하기 보다는 전체적인 흐름을 이해하는 것에 중점을 뒀다. 그것이 기억을 하기도 편하고 전체적인 흐름을 이해하는 것이 진정하게 이해를 했다라고 생각하기도 때문이다. 밑에 오늘 공부한 것에는 VPC에 대한 것이 왜 그런 것이 되는지에 대해 다른 지식과 연관지어서 써야겠다.

## 📄 배운 내용
[velog] - [[네트워크]-AWS의 VPC에 대해](https://velog.io/@ssw123/%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-AWS%EC%9D%98-VPC%EC%97%90-%EB%8C%80%ED%95%B4)


-  **vpc 자체에서 서브넷을 나눠서 사용한다**<br>
  VPC의 사설 IP 대역을 쪼개서 줄 수 있다

- **서브넷은 원하는 하나의 가용 영역을 할당 받는다**<br>
   가용 영역은 서로 독립적

- **VPC의 서브넷 아이피 대역에서는 실제 네트워크와 달리, 총 5개의 아이피 주소를 호스트에 할당 할 수 없다**<br>
>1. 첫 주소 : 서브넷의 네트워크 대역
>2. **두번째 : VPC 라우터에 할당**
>3. 세번째 : Amazon이 제공하는 DNS에 할당
>4. 미래를 위해 예약
>5. 브로드 캐스트 주소


- **vpc는 기본적으로 사설 IP**<br>
사설 IP는 그 자체로 통신이 안됨.<br>AWS로 인프라를 구축해야 통신이 가능

- **AWS의 Internet Gateway를 통해 서브넷을 퍼블릭 서브넷이 되도록 할 수 있다**.<br>
→ 서브넷을 인터넷 게이트웨이를 통해 밖으로 나가도록
라우팅 테이블 설정을 해야함<br>
→ 네트워크 패킷이 이동할 때 특정방향으로 가게 하는 것이 라우팅이기에

- **VPC 내부적으로 라우터가 있다**<br>
→ VPC 내부 서브넷끼리 통신이 가능함<br>
→ 다로 다른 서브넷은 서로 다른 LAN (서로 다른 네트워크 대역)<br>
→ 라우터가 있어야만 통신 가능

- **외부와 통신이 되지 않는 서브넷 대역인 Private Subnet은 같은 VPC의 서브넷은 통신이 가능하다**<br>
→아무런 조치를 취하지 않아 외부와 단절된 서브넷이 Private Subnet<br>
→ 사설 IP이므로 조치가 없으면 외부와 단절
→ VPC 내부적으로 라우터가 있으므로 같은 VPC내의 서브넷과 통신 가능