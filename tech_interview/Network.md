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


### 📌 TCP와 UDP의 차이
<details>
   <summary> 답안 </summary>
<br />

- TCP는 연결형 프로토콜로 3-way-handshaking 과정을 통해 연결을 설정합니다. 그렇기 때문에 높은 신뢰성을 보장하지만, 속도가 비교적 느리다는 단점이 있습니다.
- UDP 비연결형 프로토콜로 3-way-handshaking을 사용하지 않기 때문에 신뢰성이 떨어진다는 단점이 있습니다. 하지만 수신 여부를 확인하지 않기 때문에 속도가 빠르다는 장점이 있습니다.
- TCP는 신뢰성이 중요한 파일 교환 같은 경우에 쓰이고, UDP는 실시간성이 중요한 스트리밍에 자주 사용됩니다.

</details>
<br>
