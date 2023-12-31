# [TIL] DB Transaction과 Integrity constraints 

##  😃 잡담
오늘은 DB에 전반적인 이론에 대해 공부를 했다. 그중에서 무결성 제약 조건과, 트랜잭션에 대해 눈길이 갔는데, 내가 생각하기에는 파일 시스템의 단점을 DB가 극복하게 해준 특징이 바로 이 두개라고 생각됬기 때문이다. <br>
오늘 많은 내용을 내 개인 노션에 정리 했는데, 추후에 이렇게 정리한 것을 좀 더 다듬에서 내 벨로그에 올려야 겠다.!<br>
다시 무결성 제약 조건과 트랜 잭션에 대한 이야기를 하자면, 나름 생각한 이 두가지의 결론은 이것이다. 무결성 제약 조건으로 데이터의 정확성과 일관성을 보장할 수 있으며 트랙잭션으로 무결성을 보장할 수 있다. 오늘의 배운 내용은 이 두가지의 결론으로 다다르기 위한 내용을 위주로 쓰겠다! 어떻게 무결성 제약 조건이 데이터의 정확성과 일관성을 보장하며, 트랜잭션은 어떤 식으로 데이터의 무결성을 보장하는지 다시 한번 정리 해보며 복습하겠다

## 📄 배운 내용
### 무결성(Integrity)
> 데이터의 정확성, 일관성, 유효성, 정확성, 보안성을 보장하는 것

**무결성에 위반되는 예시**<br>
*ex) DB에 나이가 -20로 등록됨<br>
ex) 은행 DB에서 A가 B에게 송금을 했지만 A의 돈을 줄지 않고, B의 돈은 늘게 됨*

**이런 일들을 방지하기 위해 *(Data의 무결성을 위해)* 무결성 제약 조건과 트랜잭션을 사용한다!**

## Integrity constraints (무결성 제약 조건)

### 무결성 제약 조건을 사용해 데이터의 정확성과 일관성을 보장

- **개체 무결성 (Entity Integrity)**:
    
    **주 키(primary key) 필드는 NULL 값을 가질 수 없으며, 주 키 값은 모두 고유해야 함.** 
    
    → 각 레코드가 식별 가능하고 중복되지 않게 보장
    
- **참조 무결성 (Referential Integrity)**:
    
    관계형 데이터베이스에서 사용되며, 부모 테이블의 외래 키(foreign key)와 자식 테이블의 외래 키 간의 일관성을 보장. 
    
    **부모 테이블의 특정 값을 참조하는 모든 자식 테이블의 레코드가 항상 유효한 값을 참조**해야 함

    → *주문 테이블의 외래 키로 제품 테이블의 제품 ID를 가지며, 주문 데이터는 항상 유효한 제품 ID를 참조해야 한다.*
    
- **도메인 무결성 (Domain Integrity)**:
    
    각 **열(column)은 특정 도메인 또는 데이터 유형과 일치**해야 하며, **해당 도메인에 지정된 규칙을 따라야** 합니다. 
    
    *→ 숫자 필드는 숫자만 포함*
    
- **무결성 규칙 (Check Constraint)**:
    
    특정 열 또는 테이블에 대한 사용자 정의 규칙을 정의하는 것으로, 데이터 값의 유효성을 검사. 
    
    *→ 나이 열에 0 미만의 값을 허용하지 않는 규칙을 정의할 수 있음*
    
    *→ 계좌 잔고는 항상 0 이상이어야 한다는 규칙을 설정할 수 있음*
    
    <br>

### 실제로의 무결성 제약 조건 사용


<br>

## Transaction (트랜잭션)
> 데이터베이스의 상태를 변화시키는 논리적인 작업 단위
> 

*데이터베이스의 상태를 변화시키는 작업 단위*

*→ 데이터베이스에 접근하여 데이터를 읽고, 쓰고, 수정하고, 삭제하는 등의 작업*

### 트랜잭션의 조건

- 단일 트랜잭션은 데이터베이스에 읽거나 쓰는 등의 작업을 수행하는 여러 개의 쿼리를 요구
- 트랜잭션을 수행하면서 쿼리의 일부만 수행되는 일은 없음
- 모든 작업이 완벽하게 처리되거나 또는 처리되지 못하는 경우 원상태로 복구 됨

### 트랜잭션을 조작하여 DB의 무결성(Integrity)를 유지

**1. 원자성 (Atomicity):**<br>
트랜잭션은 데이터베이스 작업의 최소 단위이며, 트랜잭션 내의 모든 작업은 완벽하게 수행되거나 아예 수행되지 않아야 한다. 트랜잭션 중간에 문제가 발생하면 이전 상태로 롤백(원복)되어야 하며, 이것은 트랜잭션이 논리적인 작업 단위로 정의되고 일부만 수행되는 것을 방지함.

**2. 일관성 (Consistency):**<br>
트랜잭션이 완료된 후에도 데이터베이스의 상태는 트랜잭션 이전과 일관성을 유지해야 한다. 트랜잭션 도중에 다른 작업이 데이터를 변경해도 트랜잭션은 변경된 데이터를 참조하지 않고 일관된 데이터로 작업해야 한다.

**3. 고립성 (Isolation):**<br>
각각의 트랜잭션은 서로에게 영향을 주지 않고 독립적으로 실행되어야 한다. 즉, 한 트랜잭션의 작업이 다른 트랜잭션에게 미치는 영향이 없어야 함. 다른 트랜잭션이 진행 중인 데이터를 참조하지 못하고, 변경된 데이터를 공유하지 않아야 한다.

**4. 지속성 (Durability):**<br>
트랜잭션이 성공적으로 완료되면 해당 작업 결과가 영구적으로 데이터베이스에 저장되어야 한다. 시스템 장애 또는 중단 상황에서도 트랜잭션의 결과는 보존되어야 한다.

<br>

### 실제로의 트랜잭션

트랜잭션을 Commit(확정) 또는 Rollback(취소)하는 데 사용됩니다.

- **Commit:** 트랜잭션의 모든 작업이 성공적으로 수행되고 데이터베이스가 업데이트되어야 할 때 사용함. Commit을 실행하면 트랜잭션 결과가 영구적으로 저장된다.
- **Rollback:** 트랜잭션 중에 오류가 발생하거나 트랜잭션을 취소해야 할 때 사용함. Rollback을 실행하면 트랜잭션 중에 수행한 모든 작업이 취소되고 데이터베이스는 트랜잭션 이전 상태로 원상 복구됨.

**트랜잭션의 상태:**

- **Active:** 트랜잭션이 활성 상태로 실행 중인 상태
- **Failed:** 트랜잭션 실행 중에 오류가 발생하여 더 이상 진행할 수 없는 상태
- **Partially Committed:** 트랜잭션의 Commit 명령이 도착한 상태로, 아직 완전히 Commit되지 않은 상태
- **Aborted:** 트랜잭션이 취소되고 Rollback 작업을 수행하여 이전 상태로 돌아간 상태
- **Committed:** 트랜잭션이 완료되고 모든 작업이 성공적으로 Commit된 상태

- **Deadlock (교착 상태):**
여러 트랜잭션이 서로의 작업이 끝나기를 기다리며 진행하지 못하는 상황<br>
이러한 상황을 방지하기 위해 트랜잭션을 커밋하거나 트랜잭션 실행 순서를 조절하여 교착 상태를 피할 수 있다. 또한 lock을 사용하여 동시에 여러 트랜잭션이 동일한 자원에 접근하지 못하도록 제어할 수 있다.