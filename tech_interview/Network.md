# Network
<br>

### 📌 HTTP와 HTTPS의 차이
<details>
   <summary> 답안 </summary>
<br />

- HTTP는 정보를 주고 받기 위해 사용되는 프로토콜입니다. HTTP는 평문 데이터를 전송하기 때문에 HTTP로 비밀번호나 주민번호 등 중요한 정보를 주고 받으면 제 3자에 의해 조회될 수 있습니다. 이러한 문제를 해결하기 위해 HTTP에 암호화를 추가한 것이 HTTPS 입니다. 
- HTTPS는 암호화 및 인증이 있는 HTTP입니다. HTTPS는 TLS(SSL)를 사용하여 일반 HTTP 요청과 응답을 암호화하고 해당 요청과 응답에 디지털 서명을 합니다.

  <details>
   <summary> <strong> TLS란? </strong> </summary>
  <br />
     
  - TLS(전송 보안 계층)은 SSL이라는 암호화 프로토콜에서 발전한 것입니다. 
    인터넷 커뮤니케이션을 위한 개인 정보와 데이터 보안을 용이하게 하기 위해 설계된 보안 프로토콜 입니다.
  </details>
  <br>
  
</details>
<br>

### 📌 HTTP Method
<details>
   <summary> 답안 </summary>
<br />

- http method란 클라이언트가 서버한테 주어진 리소스를 가지고 수행해야 할 동작을 지정하여 요청(request)을 보내는 방식입니다.
  http method 종류는 `GET`, `POST`, `PUT`, `DELETE`, `PATCH`가 있습니다. <br>
  <br>
  - `GET`과 `POST`의 차이 : `GET`은 리소스를 조회할 때 사용하며, `POST`는 전달한 데이터의 처리/ 리소스 생성을 요청할 때 사용되는 메서드입니다.
  - `POST`와 `PUT`, `PATCH`의 차이 : `POST`는 주로 리소스를 생성하는데 사용되며, `PUT`은 리소스를 대체(수정)하거나 해당 리소스가 없으면 새로 생성 시켜주며,
     `PATCH`는 리소스의 일부분 변경을 위해 사용합니다. (PUT : 리소스 덮어쓰기 (전체 변경), PATCH : 리소스 일부 변경)
</details>
<br>

### 📌 TCP와 UDP의 차이
<details>
   <summary> 답안 </summary>
<br />

- TCP는 연결형 프로토콜로 3-way-handshaking 과정을 통해 연결을 설정합니다. 그렇기 때문에 높은 신뢰성을 보장하지만, 속도가 비교적 느리다는 단점이 있습니다.
- UDP 비연결형 프로토콜로 3-way-handshaking을 사용하지 않기 때문에 신뢰성이 떨어진다는 단점이 있습니다. 하지만 수신 여부를 확인하지 않기 때문에 속도가 빠르다는 장점이 있습니다.
- TCP는 신뢰성이 중요한 파일 교환 같은 경우에 쓰이고, UDP는 실시간성이 중요한 스트리밍에 자주 사용됩니다.

</details>
<br>


### 📌 DNS란?
<details>
   <summary> 답안 </summary>
<br />

- DNS(Domain Name System)은 사용자에게 친숙한 도메인 이름을 컴퓨터가 네트워크에서
  서로 식별하는데 사용하는 인터넷 프로토콜(IP) 주소로 변환해주는 시스템입니다. 

</details>
<br>
