# Network
<br>

### 📌 HTTP와 HTTPS의 차이
<details>
   <summary> 답안 </summary>
<br />

- HTTP는 평문 데이터를 전송하는 프로토콜이기 때문에 HTTP로 비밀번호나 주민번호 등 중요한 정보를 주고 받으면 제 3자에 의해 조회될 수 있습니다. 이러한 문제를 해결하기 위해
  HTTP에 암호화를 추가한 것이 HTTPS 입니다. 
- HTTPS에는 대칭키 암호화와 비대칭키 암호화가 모두 사용됩니다. 비대칭키 암/복호화는 비용이 매우 크기 때문에 서버와 클라이언트가 주고받는
  모든 메세지를 비대칭키로 암호화하면 오버헤드가 발생할 수 있습니다. 그래서 서버와 클라이언트가 최초 1회로 서로 대칭키를 공유하기 위한 과정에서 비대칭키 암호화를 사용하고
  이후에 메세지를 주고 받을 때에는 대칭키 암호화를 사용합니다.
</details>
<br>