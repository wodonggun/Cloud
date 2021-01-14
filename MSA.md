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

tar xvf order.tar
unzip order.zip



# -------------3일차--------------------

# docker 

이미지 : 찍어내는 틀
컨테이너 : 찍어낸 내용물


`docker` : 

- docker image pull nginx
- docker images
- docker run --name my-nginx -d -p 80:80 nginx
- docker container ls

컨테이너 명령어
1. ㅇdocker container stop `타깃`
2. docker container start `타깃`
3. 


## Docker 생성 순서

1. Docker 폴더생성
2. index.html 생성
3. Dockerfile 파일생성
  - 내부에 FROM ghcr.io/gkedu/nginx
           COPY index.html /usr/share/nginx/html/
4. docker build -t wodonggun/my-nginx:v1
5. docker login
6. docker push wodonggun/my-nginx:v1
7. docker run --name=my-first-container -d -p 8080:80 wodonggun/my-nginx:v1                컨테이너는 기본포트가 8080이고, 8080으로 들어와서 내부의80번 포트를 포워딩해줌.


## 자바파일 생성
1. 해당 자바폴더로 이동하여 mvn package   (order 폴더에서 진행함)
2. 




# --------MSA Cloud 시험---------

MSA는 
1. 중복을 허용함
2. event driven
3. 스파게티 네트워크 = 동기화(원래는 다르지만 예시로) 
4. 비동기화가 MSA다.
5. CQRS 패턴
6. MSA 



프론트엔드 => 서버사이드 렌더링 = 다 조합하고 빌드해서 배포함.
MSA는 클라이언트사이드 렌더링을 진행함.

게이트웨이 = 모든 서비스의 IP와 주소 정보 dns를 등록하지 않음. 
DDD(도메인 드리븐 ) = 


DB의 직관성,신뢰성 등 필요한 프로젝트는 하면 안됨.

카프카는 메시지큐로서 씀.(퍼포먼스가 좋음 = 다이렉트 호출만큼)

MSA의 처음 허들이 있음.
고려할게 많고, 


주문과 상품 = 메인도메인 = 코어시스템(중요한 시스템)
서포팅도메인 = 상품후기,배송시스템 등 부가적인거(서포티브)
제너럴 도메인 = 물류시스템, 결제서비스 등 우리가 굳이 개발하지않고, 갔다 쓸 수 있는것들.


ACL = 모노리식 시스템을 MSA로 변경해갈때, 접점에 있는 영역 (코어 도메인과 ACL은 어울리지 않음)


# -----4일차------------

CI - CRS종착역
CD = 쿠버네티스가 종착역



skcc10@gkn2019hotmail.onmicrosoft.com
Skccadmin!234


-리소스그룹 : skcc10-rsrcgrp
-클러스트이름 : skcc10-aks
- 컨테이너 레지스트리 : skcc10
- 이미지 Prefix =  skcc10.azurecr.io


az aks update -n skcc10-aks -g skcc10-rsrcgrp --attach-acr skcc10

kubectl get all

az aks get-credentials --resource-group skcc10-rsrcgrp --name skcc10-aks

kubectl create deployment my-nginx --image=wodonggun/my-nginx:v1

kubectl get all

kubectl expose deployment my-nginx --type=LoadBalancer --port=80   (L4 라우터의 포트임)

kubectl get all

kubectl delete service/my-nginx

http://52.141.56.224 (Externel IP 입력)


kubectl delete deploy.service --all   (전체서비스 종료)



deploy monolith --image=skcc10.azurecer.io/monolith:$(Build.BuildId)






copy files to
publish build artfiacts

copy를 Maven.pom 밑으로
Publish Artifact:drop을 copy밑으로
Copy클릭 
교재 63 페이지, Copy Files Task 속성정보
Source Folder    : $(system.defaultworkingdirectory)
Contents    : azure/*
Target Folder : $(build.artifactstagingdirectory)


Publish Artfact:drop폴더에 contents에 azure/*로 설정.



그다음
CI파이프라인 이름을 
Relaese에 CD 이름도 같게 만듬(CI를 CD로만)

kubectl 추가.
kubectl Create수정 -> Commnad를 apply로 수정, Arguments 내용 삭제, Use Configuration 체크.






RElaese -> All pipelines(그림) -> stage1글씨아래클릭 -> Cubectl Add -> 
kubectl Create : Command를 apply로, Arguments삭제, Use Configuration type 체크, File path옆에 ...클릭 -> skcc10의 drop의 azure의 deploy.yml클릭

두번째 Kubectl클릭 : kubernate service connection을 aks로 
command를 apply로, user configuration체크 
File path를 Drop,azure,service.yaml를 클릭.

Agent job+클릭 -> bash클릭 -> Display name=Bash Script, Type=inline

kubectl apply에서  File path에서 $(System.Default부터 monolith-CI까지 복사. 

sed -i “s/latest/$(Build.BuildId)/g” $(System.DefaultWorkingDirectory)/"여기에복사붙여"/drop/azure/deploy.yaml

Bash Script -> Script에 위에내용 붙여넣기. 

monolith readme수정.





--------이론

1. 


블루그린 - 묶어서 라우팅을 바꾸는거 
CI/CD = 지속적인 통합, 지속적인 배포





