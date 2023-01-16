# Cloud


## MSA란?

- MSA(Micro Service Architecture) : 

Event Store = 메세지큐

- DDD(Domain Driven Design) : 도메인주도설계
- Event Storming : DDD를 쉽게 하는 방법론(고객이 주도적으로 비지니스를 설계)



## Event Storming

![image](https://user-images.githubusercontent.com/35188271/212582810-7bae5405-6e3e-456c-9331-f79d03b3714e.png)





# 1일차

- Event Sourcing : 데이터 저장 방식 중 하나로 발생한 이벤트를 저장하는 기법. (이벤트 소싱은 클라우드에서 구동되는 메시지 중심의 분산 시스템에 적합)  
> 기존 데이터 저장 방식은 트랜잭션을 통해 바로 DB에 저장하지만, 이벤트 소싱을 통해 서비스간   
서비스는 이벤트를 발생시키고, event store(메세지큐)에 저장  
이벤트 컨슈머가 해당 이벤트를 들어온 순서대로 DB나 HDFS에 적재하고 필요 데이터를 변경함.

![image](https://user-images.githubusercontent.com/35188271/208811477-f4379185-b81c-4317-805c-e1c2ca573507.png)

![image](https://user-images.githubusercontent.com/35188271/209038040-3404852f-3631-4ffa-8825-45a3298f450f.png)



# 2일차

![image](https://user-images.githubusercontent.com/35188271/209037923-e6dee535-062b-43e4-810e-51f674cea3f1.png)

- 구글 드라이브 이벤트스토밍 : 
![image](https://user-images.githubusercontent.com/35188271/209058090-dc19863f-6574-4915-929b-8c7eaa49c38e.png)

- 음식 배달 서비스(이벤트 스토밍) : 
```
Food Delivery 예제
아래 기능적, 비기능적 요구사항을 충족하도록 시나리오대로 이벤트스토밍을 수행하시오.
(Eventstorming 수준: Design Level)

기능적 요구사항
고객이 메뉴를 선택하고, 선택한 메뉴에 대해 결제함으로써 주문이 발생한다.
주문이 되면 입점 상점주에게 주문정보가 전달된다.
상점주는 주문을 수락하거나 거절할 수 있다.
상점주는 요리 시작시와 완료 시점에 시스템에 상태를 입력한다.
고객은 아직 요리가 시작되지 않은 주문을 취소할 수 있다.
요리가 시작되면 고객 지역 인근의 라이더들에 의해 배송건 조회가 가능하다.
라이더가 해당 요리를 Pick한 후, 출발전 앱에 등록하면 배송시작 정보가 앱을 통해 고객에게 통보된다.
고객은 주문상태를 중간중간 조회한다.
시스템은 주문상태가 바뀔 때 마다 카톡으로 알림을 발송한다.
라이더가 요리를 전달한뒤 배송확인 버튼을 탭하여, 모든 거래가 완료된다.

비기능적 요구사항
장애격리
상점관리 기능이 수행되지 않더라도 주문은 365일 24시간 받을 수 있어야 한다 Async (event-driven), Eventual Consistency
결제시스템이 과중되면 사용자를 잠시동안 받지 않고 결제를 잠시후에 하도록 유도한다 Circuit breaker, fallback

성능
고객이 자주 상점관리에서 확인할 수 있는 배달상태를 주문시스템(프론트엔드)에서 확인할 수 있어야 한다 CQRS
배달상태가 바뀔때마다 카톡 등으로 알림을 줄 수 있어야 한다 Event driven

바운디드 컨텍스트
front  
store  
rider  
customer 
```
![image](https://user-images.githubusercontent.com/35188271/209084107-e720f2e8-7455-4e99-8b8e-2df270eee96a.png)



----------------------------------------------------------------------------------------------------------------


