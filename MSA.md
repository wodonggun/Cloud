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
