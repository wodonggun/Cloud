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
 
 
 

## KAFKA-CDC

```
git clone https://github.com/acmexii/kafka-connect.git
cd kafka-connect
mkdir ./h2  
cp h2.zip ./h2
cd h2
unzip h2.zip 
cd ./h2/bin
chmod 755 h2.sh
./h2.sh -webPort 8087 -tcpPort 9099
Ports탭에서 8087port 열기


```


- 쿼리 기반 CDC (Delete 동기화 불가능)
✅ 일반적으로 설정하기가 더 쉽습니다. 애플리케이션이나 좋아하는 데이터베이스 개발 도구에서 JDBC 쿼리를 실행하는 것과 마찬가지로 데이터베이스에 대한 JDBC 연결일 뿐입니다.
✅ 더 적은 권한 필요: 데이터베이스만 쿼리하므로 테이블에 대한 액세스 권한이 있는 일반 읽기 전용 사용자만 있으면 됩니다.
🛑 변경 사항을 추적하려면 소스 스키마의 특정 열이 필요합니다 . 타임스탬프 또는 증가하는 ID 필드를 포함하도록 스키마를 수정하는 옵션이 없으면 삶이 다소 어려워집니다.
🛑 데이터베이스 폴링의 영향(또는 대기 시간이 더 긴 트레이드 오프): 데이터베이스에 대해 동일한 쿼리를 너무 자주 실행하면 DBA가 전화로 무슨 일이 일어나고 있는지 물어볼 것입니다. 그러나 폴링을 너무 드물게 설정하면 오래되어 잠재적으로 덜 유용한 데이터로 끝납니다.
🛑 DELETE를 추적할 수 없음: 지금 있는 데이터에 대해서만 관계형 데이터베이스를 쿼리할 수 있습니다. 데이터가 삭제된 경우 쿼리할 수 없으므로 해당 이벤트를 Apache Kafka로 캡처할 수 없습니다.
🛑 폴링 간격 사이에 여러 이벤트를 추적할 수 없음: 커넥터가 폴링하는 기간 동안 행이 여러 번 변경되면 최신 상태만 캡처합니다. 경우에 따라 이것은 중요하지 않을 수 있습니다(단지 테이블의 최신 상태를 원하는 경우). 다른 경우에는 매우 중요할 수 있습니다(데이터베이스에서 발생하는 변경 사항에 따라 구동되는 애플리케이션을 구축하는 경우).

- 로그 기반 CDC (Delete 동기화 가능)
✅ 데이터 충실도 향상: 삽입, 업데이트, 심지어 DELETE까지 모든 것이 캡처됩니다. 이들 각각에 대해 변경된 행의 이전 상태를 가져올 수도 있습니다.
✅ 대기 시간 단축 및 소스 데이터베이스에 미치는 영향 감소: 데이터베이스 를 폴링하지 않고 트랜잭션 로그를 읽기 때문에 대기 시간이 짧고 데이터베이스에 대한 부하도 적습니다.
🛑 더 많은 설정 단계와 더 높은 시스템 권한 필요: 트랜잭션 로그는 데이터베이스의 상대적으로 낮은 수준의 구성 요소이므로 API에 액세스하려면 데이터베이스에서 더 큰 권한이 필요하며 설정이 더 복잡할 수 있습니다.



- 카프카 오류 : Broker may not been available(카프카서버 안올라감 or 찾을 수 없음)
![image](https://user-images.githubusercontent.com/35188271/213095798-5c56bc01-2834-4f4f-8003-416bbba36144.png)


```
oauth에는 Client과 Resource Server 가 있는데
gateway에서는 Client만 가지고 
각 MicroService에서는 Resource Server를 가지고있어야함.
```
![image](https://user-images.githubusercontent.com/35188271/213109582-b1de72a7-3c49-413c-a9d9-4b46804e693b.png)
