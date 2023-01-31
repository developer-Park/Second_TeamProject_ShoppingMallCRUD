
# 777 Team Lucky Seven 
>**“Customer, seller matching transaction service”**

<div>
 <img src="https://img.shields.io/badge/Java-007396?style=for-the-badge&logo=openjdk&logoColor=white">
 <img src="https://img.shields.io/badge/Gradle-02303A.svg?style=for-the-badge&logo=Gradle&logoColor=white">
  <img src="https://img.shields.io/badge/spring-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
 <img src="https://img.shields.io/badge/spring boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white">
 <img src="https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logo=Spring-Security&logoColor=white">
</div>
<div>
 <img src="https://img.shields.io/badge/Hibernate-59666C?style=for-the-badge&logo=Hibernate&logoColor=white">
 <img src="https://img.shields.io/badge/redis-%23DD0031.svg?&style=for-the-badge&logo=redis&logoColor=white">
 </div>
<div>
 <img src="https://img.shields.io/badge/IntelliJ_IDEA-000000.svg?style=for-the-badge&logo=intellij-idea&logoColor=white"><img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
<img src="https://img.shields.io/badge/postman-FF6C37?style=for-the-badge&logo=postman&logoColor=white">
</div>

## 목차

<!-- TOC -->
* [💻 Project development environment](#💻)
* [👥 Team Members](#Team-Members)
    * [Role](#Role)
* [Project requirement](#Project-requirement)
* [Usecase](#usecase)
* [Table ERD](#table-erd)
* [Class UML](#class-uml)
* [API details](#api-details)
<!-- TOC -->


<br>


## 💻
<details><summary> &nbsp Project development environment</summary>

- spring 2.7.6
- h2
- JDK 17
- build.gradle
    ```
   dependencies {
        implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
        implementation 'org.springframework.boot:spring-boot-starter-security'
        implementation 'org.springframework.boot:spring-boot-starter-web'
        implementation 'org.springframework.boot:spring-boot-starter-validation'
    
        compileOnly 'org.projectlombok:lombok'
        runtimeOnly 'com.h2database:h2'
        annotationProcessor 'org.projectlombok:lombok'
    
        testImplementation 'org.springframework.boot:spring-boot-starter-test'
        testImplementation 'org.springframework.security:spring-security-test'
    
        testCompileOnly 'org.projectlombok:lombok'
        testAnnotationProcessor 'org.projectlombok:lombok'
    
    
        compileOnly group: 'io.jsonwebtoken', name: 'jjwt-api', version: '0.11.2'
        runtimeOnly group: 'io.jsonwebtoken', name: 'jjwt-impl', version: '0.11.2'
        runtimeOnly group: 'io.jsonwebtoken', name: 'jjwt-jackson', version: '0.11.2'
    
        implementation 'org.springframework.boot:spring-boot-starter-data-redis'
        implementation group: 'it.ozimov', name: 'embedded-redis', version: '0.7.1'
    
        implementation 'org.springframework.boot:spring-boot-starter-websocket'
    }
    ```

- application.properties

  ```
  spring.h2.console.enabled=true
spring.datasource.url=jdbc:h2:mem:db;MODE=MYSQL;
spring.datasource.username=
spring.datasource.password=

spring.thymeleaf.cache=false

spring.jpa.properties.hibernate.show_sql=true
logging.level.org.hibernate.type.descriptor.sql=trace

jwt.secret.key=

##Redis
spring.redis.host=localhost
spring.redis.port=6379

##Swagger
spring.mvc.pathmatch.matching-strategy=ant_path_matcher

    ```
</details>
<br>

## 👥 Team Members
JeongHun Park(Parker), Mun ji Young, Ji seop Lee, Hyun jae Jang


### Role

| Manager | Role                                                                          |
|:---:|:----------------------------------------------------------------------------|
|     |                                                                             |
| Parker | - Spring Security,JWT Token,Redis<br/>- Signup,Signin,Logout<br/>- Category section,User section,Point section<br/>- Exception section, HTML|
| Mun ji Young | -  시큐리티<br/>- 회원가입 / 로그인<br/>-  로그아웃<br/>- 프로필 설정/조회<br/>- 리드미 작성           |
| Ji seop Lee | - 전체 판매 상품 조회<br/>- 판매자 등록 상품 조회/검색/등록/수정/삭제(판매자 포함)<br/>- 채팅<br/>- 프로젝트 발표 |
| Hyun jae Jang | - 시큐리티(리프레시 토큰)<br/>-  레디스 적용<br/>- 카테고리 조회/생성/수정/삭제                        |
| | - 거래 조회/요청/수락<br/>- 판매자 조회<br/>- 프로필 이미지 저장/조회<br/>- 시연 영상 제작               |


<br>

## Project requirement
<details><summary> details
</summary>- Creating our own matching service project
[ Customer-seller matching service (free matching subject)]
- Member signup/login/logout/token function
- User permission function
    - Users are divided into three rights.
        - Customer: The user who first registered as a member
        - Seller: Customers who have been approved as a seller
        - Operator: User who approves the seller
- Functions by user authority
    - customer
        - Lookup
            - My profile setting and inquiry: You can set and view profiles (nickname, image) for each user
            - List of all sales products: Paging through the list of sales products
            - List of all sellers: search through the list of sellers by paging
            - Seller information: Select a seller to view profile information (nickname, image, introduction + matching topic information)
        - write
            - Request Form to Seller: Send the request details (matching topic information) to the seller
        - Permission request
            - Seller registration request: Fill out the seller profile request information and request seller registration to the operator
            
    - seller
        - Lookup
            - Set and view my seller profile: set and search profile for each seller (nickname, image, introduction + matching topic information)
            - Search my sales products: Paging through the list of products I am selling
            - Search customer request list: Paging and search the customer request list of all products
        - Enrollment
            - Register my sales product: Fill out the sales product information and register it on the list
        - Modify
            - Modify/Delete My Selling Products: Write the selling product information and edit it in the list
        - delete
            - Delete my sales product: Write the sales product information and delete it from the list
        - Customer request processing: Accept customer request and complete processing
    - Operator
        - Lookup
            - Customer List: Paging through the list of customers
            - Seller List: Paging and search the list of sellers
            - Seller registration request form list: Search the seller registration request list
        - Permission registration
            - Seller permission approval: Approve the seller registration request
        - delete
            - Seller authority: Delete user's seller authority
            
- Search function
    - Keyword search: Add a search function by entering a search keyword when searching for paging lists.
    - Seller Search: Add a function to search by seller name when searching the paging list.


- Customer-seller conversation function
    - Chat room creation: A chat room is created when sales start.
    - Conversation message transmission function: Customer and seller have a conversation about the sale.
    - Chat room message list search: You can search the chat list between the customer and the seller.
    - Chat room termination: When the sale is completed, the chat room is stopped and no more messages can be sent.
    
</details>

<br>

## Usecase
![Usecase.png](document/usecase.png)

<br>

## Table ERD
![TableERD.png](document/TableERD.png)

<br>

## Class UML
![ClassUML.png](document/ClassUML.png)

## API details
![img.png](document/UserAPI.png)

![img.png](document/AdminAPI.png)

![img.png](document/ItemAPI.png)

![img.png](document/TransactionAPI.png)

![img.png](document/CategoryAPI.png)

![img.png](document/ChatAPI.png)













