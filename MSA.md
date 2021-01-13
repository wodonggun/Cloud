# MSA

1. 스프링 접속 : https://start.spring.io/
2. Maven Project -> java -> 버전2.4.1 -> jar -> java ver8
3. Dependency : Srping Data JPA, Rest Repositories HAL Explorer, H2 Database 
4. ㅁㄴㅇㄹ




1. msaez.io에서 PROJECT익프로러에서 우측마우스 -> Demo.zip 열기.
2. 해당 폴더에서 명령어 실행 : unzip demo.zip 
3. 왼쪽 하단에 activating java dependency로딩(3~4분) 진행후 JAVA DEPENDENCIES에 demo 생성됨.



mvn spring-boot:run
netstat -anlp | grep :8080     spring 포트
netstat -anlp | grep :9092     카프카 포트



pom.xml에 카프카 디펜던시 추가(dependencies 태그 내부에)
        <!-- kafka streams -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-stream-kafka</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-actuator</artifactId>
        </dependency>
        
        

project->

pom.xml에 수정사항이 있다 -> pom.xml우측클릭 -> update project configuration.


PolicyHandler = 


yaml = 
yaml : ---표시는 하나의 문단




# 실습

1. Lab탭 -> kafka Consumer -> mall로 토픽 설정
2. 



▣ 주문/배송을 활용한 EventStorming 설계 및 CNA 구현

▣ User Stories & System Requirements 
 > 기능 요건
   - 고객이 주문을 하면, 주문정보를 바탕으로 배송이 시작된다.
   - 고객이 주문취소를 하게 되면, 주문정보는 삭제되나,
   - 배송팀에서는 (사후, 활용 위해) 취소 장부를 별도 저장한다. 
   - 주문과 배송 서비스는 게이트웨이를 통해 고객과 통신한다.  

 > 비기능 요건
   - 주문팀의 주문 취소는 반드시 배송팀 배송취소가 전제되어야 한다. 

   -------------------  (추가 기능요건)  ------------------------
   > 고객은 주문서비스에서 배송 상태를 열람할 수 있어야 한다.
   > 고객센터는 MyPage를 통해, 12st Mall의 모든 진행내역의 모니터링을 제공해야 한다. 





반드시 : 주문 취소를 요청하고, 대기해서 배송팀에 대해서 배송취소가 승인되어야 하므로써, 동기화가 필요함.

별도 저장 : 어그리게이션을 나눠서 별도 저장할 수 있도록 만듬.(Delivery,Cancellation 분리)



http localhost:8081/orders productId=100 qty=1
http localhost:8081/orders 
http DELETE localhost:8081/orders/1
http localhost:8081/orders
http localhost:8082/cancellations
http localhost:8083/mypages

