# Database
<br>

### 📌 트랜잭션

<details>
   <summary> 답안 </summary>
<br />

- 트랜잭션이란 데이터베이스 내의 최소 작업단위입니다. 트랜잭션은 ACID의 성질을 가지고 있으며, 이는 각 원자성, 일관성, 독립성, 지속성을 의미합니다. <br>
  - **원자성(Atomicity)** : 트랜잭션에 포함된 작업은 모두 수행되거나 모두 수행되지 않아야 하는 성질을 의미합니다.
  - **일관성(Consistency)** : 트랜잭션을 수행하기 전이나 후나 데이터베이스는 항상 일관된 상태를 유지하는 성질을 의미합니다.
  - **독립성(Isolation)** : 트랜잭션이 시작되면 다른 어떠한 작업도 끼어들 수 없다는 것을 의미합니다.
  - **지속성(Durability)** : 수행을 성공적으로 완료한 트랜잭션은 변경한 데이터를 영구히 저장해야 한다는 것을 의미합니다.

</details>
<br>

### 📌 트랜잭션 격리수준
<details>
   <summary> 답안 </summary>
<br />

- 트랜잭션 격리 수준(Isonlation Level)이란 **여러 트랜잭션이 동시에 처리될 때, 특정 트랜잭션이 다른 트랜잭션에서 변경하거나 조회하는 데이터를 볼 수 있게 허용할지
  여부를 결정하는 것입니다**. 트랜잭션의 격리 수준은 격리(고립) 수준이 높은 순서대로 `SERIALIZABLE`, `REPEATABLE READ`, `READ COMMITTED`, `READ UNCOMMITTED`가 존재합니다.
  - **[SERIALIZABLE]**
    - SERIALIZABLE은 이름 그대로 트랜잭션을 순차적으로 진행시킵니다. **여러 트랜잭션이 동일한 레코드에 동시에 접근할 수 없으므로**, 데이터 부정합 문제도 발생하지 않습니다.
      하지만 **트랜잭션이 순차적으로 처리되어야 하므로 동시 처리 성능이 매우 떨어집니다**. SERIALIZABLE은 가장 안전하지만, 가장 성능이 떨어지므로 극단적으로 안전한 작업이 필요한
      경우가 아니라면 사용하지 않는 것이 좋습니다.
  - **[REPEATABLE READ]**
    - REPEATABLE READ는 MySQL의 InnoDB에서 기본으로 사용하는 트랜잭션 격리 수준입니다. REPEATABLE READ는 **MVCC를 이용해 한 트랜잭션 내에서 동일한 결과를 보장하지만, 
      새로운 레코드가 추가되는 경우에 부정합이 생길 수 있습니다**. 이러한 부정합을 방지하기 위해 InnoDB는 갭락과 넥스트 키락을 활용합니다. 
  - **[READ COMMITTED]**
     - READ COMMITTED는 **커밋된 데이터만을 조회할 수 있는 격리 수준**입니다. 특정 트랜잭션에서 데이터가 변경되었으나, 아직 커밋되지 않은 상태라면 다른 트랜잭션에서는
       해당 데이터를 읽을 수 없고 커밋이 된 이후에야 변경된 데이터 값을 읽을 수 있습니다. 이러한 특성으로 **Phantom Read의 문제와 Non-Repeatable Read 문제가 발생할 수 있습니다**.
  - **[READ UNCOMMITTED]**
     - READ UNCOMMITTED는 **커밋되지 않은 데이터 조차도 접근할 수 있는 격리 수준**입니다. **데이터의 부정합 문제가 발생할 확률이 높지만, 성능은 가장 빠르다는 특징**이 있습니다.
       하여 데이터를 어림잡아 집계하는 등의 연산에 유용하게 사용됩니다.
</details>
<br>

### 📌 Commit & Rollback
<details>
   <summary> 답안 </summary>
<br />

- commit이란 한 트랜잭션 내의 모든 작업을 데이터베이스에 반영하는 작업이며, rollback이란 작업 중 문제가 발생되어
  트랜잭션의 처리과정에서 발생한 변경사항을 취소하는 명령어 입니다. 


</details>
<br>

### 📌 동시성 제어 기법 / 2PL
<details>
   <summary> 답안 </summary>
<br />

- 2-Phase-Lock(2단계 잠금 프로토콜)이란 트랜잭션 도중에 락을 걸어 동일한 데이터에 동시에 접근하려는 트랜잭션을 차단하여 직렬화를 보장하는 DBMS의 동시 제어 방법입니다.<br>
![image](https://github.com/pie2457/backend_tech_interview/assets/104147789/0b1df445-b8f6-4db7-a985-7d99edaed29c) <br>
  2PL은 각 트랜잭션이 두 단계로 락 획득 또는 해제 요청을 할 수 있습니다. <br>
  - Growing Phase : 이 단계에서는 오직 잠금을 획득할 수 있고, 해제할 수는 없습니다.
  - Shrinking Phase : 이 단계에서는 트랜잭션이 잠금을 해제할 수는 있지만, 새로운 잠금을 획득할 수는 없습니다.


</details>
<br>

### 📌 동시성 제어 기법 / Pessimistic Lock & Optimistic Lock
<details>
   <summary> 답안 </summary>
<br />

- **[Pessimistic Lock]**
   - 비관적 락은 2개 이상의 트랜잭션이 동시에 동일한 데이터에 접근할 것이라 가정하여 DB의 실제 데이터에 락을 걸어 데이터의 정합성을 맞추는 방식입니다. 비관적 락은 트랜잭션이 시작할 때 X-Lock 또는 S-Lock을 걸게 됩니다.
      - 배타 락 (Exclusive-Lock, X-Lock) : 배타 락은 엔티티에 접근하려는 모든 요청을 제어합니다. 하나의 요청이 자원을 얻으면 다른 요청은 대기 상태가 됩니다.
      - 공유 락 (Shared-Lock, S-Lock) : 공유 락은 업데이트 상황에서만 동시성 제어를 하고 있습니다. 조회만 하는 경우에는 락이 발생하지 않고 접근이 가능합니다.
- **[Optimisitic Lock]**
   - 낙관적 락은 2개 이상의 트랜잭션이 동시에 동일한 데이터에 접근하지 않을 것이라 가정하여 실제로 락을 사용하지는 않고 버전 정보를 이용해 데이터의 정합성을 맞추는 방식입니다.
     데이터에 접근할 때와 데이터를 변경하려 할 때 두 버전의 정보(ex. 접근할 때 : ver.1, 변경할 때 : ver.2)가 다르다면 rollback이 일어납니다.

</details>
<br>

### 📌 MVCC (Multi-Version Concurrency Control)

<details>
   <summary> 답안 </summary>
<br />

- MVCC는 원본의 데이터와 변경중인 데이터를 동시에 유지하는 방식으로 원본 데이터에 대한 Snapshot을 백업해 보관하여, 동시 접근을 허용하는 데이터베이스에서 동시성을 제어하기 위해 사용하는 방법 중 하나입니다. <br>
  새로운 사용자가 데이터에 접근하면 스냅샷을 읽고, 만약 변경이 취소되면 원본 스냅샷을 바탕으로 데이터를 복구하고, 변경이 완료되면 최종적으로 디스크에 반영하는 방식으로 동작합니다.<br>
  MVCC는 잠금을 필요로 하지 않기 때문에 일반적인 RDBMS보다 매우 빠르게 작동하지만, 하나의 데이터에 대한 여러 버전의 데이터를 허용하기 때문에 데이터 버전이 충돌을 일으킬 수 있습니다. <br>
  
  
</details>
<br>

### 📌 동시성을 제어하지 않았을 시 생기는 문제
<details>
   <summary> 답안 </summary>
<br />
   
   ### 1. 갱신 분실 (Lost Update)
   하나의 트랜잭션이 수행한 데이터 변경 연산이 저장되기 전에 다른 트랜잭션이 데이터를 가지고 가서 데이터를 변경하고 다시 저장하는 경우, 첫번째 트랜잭션이 수행한 연산이 무효가됩니다. 
<table>
   <tr>
      <th scope="col"> 시간 </td>
      <th scope="col"> 트랜잭션1 </td>
      <th scope="col"> 트랜잭션2 </td>
   </tr>
   <tr>
      <td> 1 </td>
      <td> select A </td>
      <td> </td>
   </tr>
   <tr>
      <td> 2 </td>
      <td>   </td>
      <td> select A </td>
   </tr>
   <tr>
      <td> 3 </td>
      <td> update A to b </td>
      <td> </td>
   </tr>
   <tr>
      <td> 4 </td>
      <td>   </td>
      <td> update A to c </td>
   </tr>
</table>
   1. 트랜잭션1에서 A 조회 (현재 A값은 a) <br>
   2. 트랜잭션2에서 A 조회 (현재 A값은 a) <br>
   3. 트랜잭션1에서 A -> b로 갱신 (현재 A값은 b) <br>
   4. 트랜잭션2에서 A -> c로 갱신 (현재 A값은 c) <br>
   -> 트랜잭션1의 갱신이 손실된다. 

   ### 2. 미완료 의존성 (Uncommited Dependency)
   한 트랜잭션이 수행 중 장애가 생겨 rollback 연산을 하기 전에 해당 트랜잭션이 갱신한 데이터를 다른 트랜잭션에서 이미 가져갔다면, 데이터베이스에 있는 데이터와 트랜잭션이 가지고 있는
   데이터가 다르게 되는 문제가 발생하게 됩니다. 
<table>
   <tr>
      <th scope="col"> 시간 </td>
      <th scope="col"> 트랜잭션1 </td>
      <th scope="col"> 트랜잭션2 </td>
   </tr>
   <tr>
      <td> 1 </td>
      <td> </td>
      <td> select A </td>
   </tr>
   <tr>
      <td> 2 </td>
      <td>   </td>
      <td> update A to b </td>
   </tr>
   <tr>
      <td> 3 </td>
      <td> select A </td>
      <td> </td>
   </tr>
   <tr>
      <td> 4 </td>
      <td>   </td>
      <td> rollback </td>
      <br>
   </tr>
</table>
   1. 트랜잭션2에서 A 조회 (현재 A값은 a) <br>
   2. 트랜잭션2에서 A -> b로 갱신 (현재 A값은 b) <br>
   3. 트랜잭션1에서 아직 완료되지 않은 갱신(비완료된 변화)을 조회 (현재 A값은 b) <br>
   4. 트랜잭션2에서 롤백 (현재 A값은 a) <br>
   -> 트랜잭션1에서는 아직 완료되지 않은 갱신(비완료된 변화)를 조회하게 된다. 

   ### 3. 모순성 (inconsistency)
   데이터 x, y에 각 100이라는 숫자가 들어있다고 가정합니다. <br>
   트랜잭션1은 x, y에 20을 더하는 연산을 수행한뒤, 트랜잭션2번이 수행이되어야 합니다.
<table>
   <tr>
      <th scope="col"> 시간 </td>
      <th scope="col"> 트랜잭션1 </td>
      <th scope="col"> 트랜잭션2 </td>
   </tr>
   <tr>
      <td> 1 </td>
      <td> select x </td>
      <td> </td>
   </tr>
   <tr>
      <td> 2 </td>
      <td> update x to value(100) + 20 </td>
      <td> </td>
   </tr>
   <tr>
      <td> 3 </td>
      <td> </td>
      <td> select x , y</td>
   </tr>
   <tr>
      <td> 4 </td>
      <td>   </td>
      <td> update x, y to value(x = 120, y = 100) * 2 </td>
   </tr>
   <tr>
      <td> 5 </td>
      <td> select y </td>
      <td> </td>
   </tr>
   <tr>
      <td> 6 </td>
      <td> update y to value(200) + 20 </td>
      <td> </td>
      <br>
   </tr>
</table>
   1. 트랜잭션1에서 x값 조회. <br>
   2. 트랜잭션1에서 x값을 x값 + 20으로 갱신. (x값=120, y값=100) <br>
   3. 트랜잭션2에서 x, y값 조회. <br>
   4. 트랜잭션2에서 x와 y값을 120, 100 * 2로 갱신 (x값=240, y값=200). <br>
   5. 트랜잭션1에서 y값 조회. <br>
   6. 트랜잭션1에서 y값을 y값 + 20으로 갱신. <br>
   -> 결과는 x값=240 y값=240이어야 하지만 동시성 제어가 없다고 가정했기 때문에 데이터의 일관성이 없어 모순이 발생하게 됩니다.
   
### 4. 연쇄 복귀 (Cascading Rollback)
트랜잭션에 장애가 발생해서 rollback 연산을 하려면 해당 트랜잭션이 사용했던 데이터를 사용한 다른 트랜잭션들도 rollback을 수행해야 하는데 이미 그 트랜잭션이 완료되어 커밋이 됐는데도 rollback이 수행되어야 해서 문제가 발생하게 됩니다. <br>
데이터 x, y에 각 100이라는 숫자가 들어있다고 가정합니다.
<table>
   <tr>
      <th scope="col"> 시간 </td>
      <th scope="col"> 트랜잭션1 </td>
      <th scope="col"> 트랜잭션2 </td>
   </tr>
   <tr>
      <td> 1 </td>
      <td> select x </td>
      <td> </td>
   </tr>
   <tr>
      <td> 2 </td>
      <td> update x to value(100) + 20 </td>
      <td> </td>
   </tr>
   <tr>
      <td> 3 </td>
      <td> </td>
      <td> select x </td>
   </tr>
   <tr>
      <td> 4 </td>
      <td>   </td>
      <td> update x to value(x = 120) * 2 </td>
   </tr>
   <tr>
      <td> 5 </td>
      <td> select y </td>
      <td> </td>
   </tr>
   <tr>
      <td> 6 </td>
      <td> 장애로 인한 rollback</td>
      <td> 이미 완료되었지만 rollback 된다</td>
   </tr>
</table>
   1. 트랜잭션1에서 x값 조회. <br>
   2. 트랜잭션1에서 x값을 x값 + 20으로 갱신. (x값=120, y값=100) <br>
   3. 트랜잭션2에서 x값 조회. <br>
   4. 트랜잭션2에서 x와 120 *2 2로 갱신. (x값=240, y값=100). <br>
   5. 트랜잭션1에서 y값 조회. <br>
   6. 트랜잭션1에서 장애로 인한 rollback 발생 -> 트랜잭션2도 rollback. <br>
   -> 트랜잭션1에서 장애가 발생해 rollback이 되어 원래 DB 상태로 복구되어야 하는데 여기서 트랜잭션1이 건드린 데이터는 x, y입니다. rollback이 발생하였으니 데이터 x도 rollback이 수행되어야 하지만, 트랜잭션2 또한 x의 데이터로 연산 작업을 수행한 후 커밋으로 데이터를 저장합니다. 장애가 발생하여 x, y 데이터 모두 원래 상태로 복구되어야 하지만 
트랜잭션2가 이미 완료된 트랜잭션이기 때문에 rollback 연산을 할 수 없게 되어 문제가 발생합니다. 
   
</details>
<br>

### 📌 데이터베이스 무결성 제약조건

<details>
   <summary> 답안 </summary>
<br />

- 무결성 제약조건이란 데이터베이스의 정확성, 일관성을 보장하기 위해 저장, 삭제, 수정 등을 제약하기 위한 조건을 뜻합니다. 무결성 제약조건은 크게  <br>`도메인 무결성 제약조건`, `개체 무결성 제약조건`, `참조 무결성 제약조건`이 있습니다. <br>
  - 도메인 무결성 제약조건 : 각 속성의 값은 반드시 도메인에 지정된 값만을 가져야 한다는 조건입니다.
     - ex ) 성별의 속성은 `남` & `여`로만 이루어져야 합니다.  
  - 개체 무결성 제약조건 : 기본키로 정의한 속성은 항상 NULL값을 가질 수 없다는 규칙입니다.
     - ex ) 직원 명단을 관리하려할 때 `사번`이 기본키로 정의되어 있으면, `주소`나 `직책` 속성은 입력하지 않아도 `사번`은 반드시 값을 입력해야한다는 의미입니다. 
  - 참조 무결성 제약조건 : 관계 대응이 안되는 외래 키 값을 가질 수 없다는 규칙입니다.
     - ex ) 멤버 테이블이 팀 테이블을 외래 키로 가지고 있을 때, 멤버 테이블에서 팀 넘버라는 속성은 팀 테이블에서 가지고 있는 기본 키의 속성이 아니면 안된다는 의미입니다. <br>
            (팀 테이블은 1개의 팀만 가지고 있어 기본 키가 1로 설정 되어있는데 멤버 테이블에서 팀 넘버라는 속성이 2라고 되어있으면 안됨.)

</details>
<br>

### 📌 조인 (Join)
<details>
   <summary> 답안 </summary>
<br />
   
- 조인이란 두 개 이상의 테이블을 연결하여 하나의 결과를 만들어 내는 것을 의미하며, 이를 통해 데이터를 효율적으로 검색하고 처리하는데 도움을 줍니다. <br>
  ### 조인의 종류
  - InnerJoin : 두 테이블을 연결할 때 가장 많이 사용하는 것이 inner join입니다. 기준 테이블과 join한 테이블의 중복값을 보여줍니다. <br>
    <img src="https://hongong.hanbit.co.kr/wp-content/uploads/2021/11/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-SQL_INNER-JOIN.png" style="width: 30%; height: auto;"> 

  - Left Outer Join : 기준 테이블은 다 보여주고 join 테이블은 기준 테이블과 중복된 값을 보여줍니다. 기준 테이블과의 중복값이 없다면 Null로 표기됩니다. <br>
  - Right Outer Join : Left Outer Join 반대. <br>
   <img src="https://hongong.hanbit.co.kr/wp-content/uploads/2021/11/%ED%98%BC%EC%9E%90-%EA%B3%B5%EB%B6%80%ED%95%98%EB%8A%94-SQL_OUTER-JOIN.png" style="width: 30%; height: auto;"> 

[사진 출처] : https://hongong.hanbit.co.kr/sql-%EA%B8%B0%EB%B3%B8-%EB%AC%B8%EB%B2%95-joininner-outer-cross-self-join/
</details>
<br>
