# Development 

- Policy 코멘트  
![image](https://user-images.githubusercontent.com/35188271/212603784-9cc909e4-e0db-4b7a-b9d2-6190ba455ccd.png)


- spring boot 코드 : https://start.spring.io/  
![image](https://user-images.githubusercontent.com/35188271/212606592-fc19710d-21b3-4b37-b5c3-43be7847387d.png)
  
```
Middleware = Oracle
Binder = ORM Mapper
```
![image](https://user-images.githubusercontent.com/35188271/212617287-06857972-3a78-4d65-8fd4-fa3b516e205f.png)




- `./kafka-console-consumer --bootstrap-server localhost:9092 --topic shop  --from-beginning` : from Beggining옵션은 기존 카프카에 누적된 모든 메세지를 다 읽어옴.
실행시점부터 누적하고 싶다면 해당 옵션을 빼면됨.




# 2일차

![image](https://user-images.githubusercontent.com/35188271/212785489-29ab924f-618a-4412-b7c6-b0422b70f4c4.png)
![image](https://user-images.githubusercontent.com/35188271/212785503-e1080523-e2ed-439d-b902-3b7a298bf2dc.png)
![image](https://user-images.githubusercontent.com/35188271/212785836-36666160-4df5-4275-93b2-e3ae15f50cb4.png)
![image](https://user-images.githubusercontent.com/35188271/212785844-b44711c7-6c95-457f-9c4b-34fcc91abf15.png)




- `API Gateway` : 로드밸런싱, 통합인증(보안)에 장점을 가지고있음.  
![image](https://user-images.githubusercontent.com/35188271/212787550-fa994c20-d435-4dcf-a286-bd3f25e2bb48.png)

- `Service Registry` : API Gateway가 클러스터 내의 인스턴스를 찾아가는 앱(Eureka, kube-DNS)
![image](https://user-images.githubusercontent.com/35188271/212788448-09c6ea9f-c543-4856-a3dd-901b8f0bebdb.png)

- `CDC(Change Data Capture)` : 카프카에서 지원하는 DB의 변화를 모니터링하고, 데이터 동기화를 위해 이벤트(알림)을 발행함.  
기존 레거시에서 DB에 접속해서 변경사항을 이벤트로 발행하여 레거시+MSA 통합으로 사용, CQRS 읽기 모델 동기화용으로 사용.
![image](https://user-images.githubusercontent.com/35188271/212799342-0bbdc51b-67c6-40f5-b344-ff225745f7c1.png)





## `레거시 전환`
![image](https://user-images.githubusercontent.com/35188271/212791496-92eb723b-5b0b-4f4c-9226-9f16acb3865d.png)


![image](https://user-images.githubusercontent.com/35188271/212791984-ecc5d458-d6a8-4c97-8435-a09bdf93533a.png)
![image](https://user-images.githubusercontent.com/35188271/212792161-ffb7228d-d76b-4fc5-95f8-3bce3c10001c.png)

- `카프카`: Topic(접근 큐), Partitions(Topic내 N개의 큐=메세지 로드밸런싱(라운드로빈방식으로 데이터 삽입)), Offsets(각 서비스마다 읽어야하는 위치를 알려줌=읽은데이터체크)
- `브로커` : 카프카 서버
- `주키퍼` : 브로커를 관리하는 오케스트레이션
- `ISR(In Sync Replica)` : 리더 브로커를 복제하여, 리더가 장애시 대체됨
- `컨슈머` : 컨슈머4개일때, 브로커를 구독하지않는다(파티션은 3개라서) = C4 마이크로서비스는 메세지를 sub하지않고 놀고있지만, 다른 로직시스템은 돌아갈 수 있음.  
![image](https://user-images.githubusercontent.com/35188271/212798589-5c0921b8-5369-48af-82de-cae6eea9e969.png)  

```
메세지 생성 -> 파티셔너가 각 파티션으로 메세지를 라운드로빈방식으로 던져줌.



```
![image](https://user-images.githubusercontent.com/35188271/212800987-3700a776-3866-4366-bf35-be87ce695924.png)


- 순서 보장 :


- `Destination` : Topic과 동일
![image](https://user-images.githubusercontent.com/35188271/212813982-cb3c5cae-cb69-48fd-8066-737aee9e5d21.png)

- `FeignClient` : 간단한 Rest API 동기 호출 클래스
- 

- `kafka 정보` : 
![image](https://user-images.githubusercontent.com/35188271/212817142-f4558abf-66b6-4c34-8cda-ae87479d11b8.png)

- `PATCH` : 부분 수정(qty만 보내면 qty만 수정됨)
- `PUT` : 전체 수정(qty만 보내면 나머지는 지워지고 qty만 update됨



# 3일차

- `리밸런싱` : Partition과 MicroService간의 오케스트레이션 처리.


메세지 순서성에 대한 실습

- 장애전파 차단 : 서킷브레이커 패턴(요청측에서 차단기를 넣고, 특정 요청시간이 넘어서면 끊어버림)
![image](https://user-images.githubusercontent.com/35188271/213056072-6162f8c8-0018-4d61-bee3-bf62a116f2c8.png)

- FallBack : 서킷브레이커 동작 또는 응답이 없을때 다른주소(오류 알림)를 보여주거나 우회 처리.  

 
 ![image](https://user-images.githubusercontent.com/35188271/213058788-d5109fcc-e07d-4e8c-a4e6-cc47880e324a.png)
 
 
 

