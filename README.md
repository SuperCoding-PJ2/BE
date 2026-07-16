AWS Image Upload Backend

Spring Boot와 AWS S3, EC2, RDS를 활용하여 이미지 업로드와 상품 관리를 구현한 쇼핑몰 백엔드 프로젝트

프로젝트 소개

이미지 업로드 기능은 대부분의 웹 서비스에서 필수적으로 사용되는 기능입니다. 본 프로젝트는 Spring Boot 기반 쇼핑몰 백엔드를 구현하고 AWS S3를 이용한 이미지 저장, EC2 기반 API 서버 운영, RDS(MySQL)를 활용한 데이터 저장 구조를 구축하였습니다.

MultipartFile 기반 이미지 업로드부터 S3 URL 생성, 상품 정보 저장, REST API 제공까지 실제 서비스 환경을 고려한 백엔드 아키텍처를 설계하였습니다.

또한 AWS 인증 정보 분리, 예외 처리, JPA Auditing 등을 적용하여 유지보수성과 보안성을 함께 고려하였습니다.

주요 기능
1. 이미지 업로드

Spring Boot의 MultipartFile을 이용하여 이미지 업로드 기능을 구현하였습니다.

업로드된 이미지는 S3Uploader를 통해 Amazon S3에 저장되며, 저장 완료 후 이미지 URL을 생성하여 반환하도록 구현하였습니다.

2. 상품 관리 API

상품 등록 API를 구현하여

상품명
가격
설명
이미지 URL

등의 정보를 함께 저장하도록 설계하였습니다.

이미지 업로드와 상품 등록이 하나의 비즈니스 로직으로 동작하도록 구성하였습니다.

3. Amazon S3 연동

AWS SDK를 활용하여 S3Uploader를 직접 구현하였습니다.

S3Client를 이용해 이미지를 업로드하고, 업로드 완료 후 접근 가능한 URL을 생성하여 데이터베이스에 저장하도록 구현하였습니다.

환경별 설정을 분리하여 유지보수성을 높였습니다.

4. Amazon RDS 연동

MySQL 기반 Amazon RDS를 데이터베이스로 사용하였습니다.

Spring Data JPA를 적용하여 상품 정보를 관리하고 이미지 URL과 함께 저장하도록 구현하였습니다.

5. REST API

RESTful API를 구현하여

상품 등록
상품 조회
이미지 업로드

기능을 제공하였습니다.

프론트엔드와 백엔드를 완전히 분리하여 API 기반 구조를 적용하였습니다.

6. JPA 기반 도메인 설계

Spring Data JPA를 활용하여 Entity와 DTO를 분리하고 계층형 구조를 적용하였습니다.

또한 BaseEntity를 적용하여 생성일과 수정일을 자동 관리하도록 구현하였습니다.

7. 예외 처리

GlobalExceptionHandler를 구현하여 예외를 일관된 형태로 반환하도록 설계하였습니다.

비즈니스 로직과 예외 처리 로직을 분리하여 유지보수성을 향상시켰습니다.

8. 보안 및 설정 관리

AWS Access Key와 Secret Key는 환경변수 및 ConfigurationProperties를 통해 관리하도록 구성하였습니다.

민감한 정보를 코드에 직접 작성하지 않고 외부 설정으로 분리하여 보안성을 높였습니다.

또한 향후 AWS Secrets Manager를 적용할 수 있도록 구조를 설계하였습니다.

9. AWS 운영 환경

애플리케이션은 Amazon EC2에서 실행되며, 이미지 파일은 Amazon S3, 데이터는 Amazon RDS에 저장되도록 구성하였습니다.

클라우드 환경을 고려한 구조를 적용하여 실제 서비스 운영 환경과 유사한 백엔드 아키텍처를 구축하였습니다.

이미지 업로드 흐름
Client
   │
   ▼
Multipart Upload
   │
   ▼
Spring Controller
   │
   ▼
Service
   │
   ▼
S3Uploader
   │
   ▼
Amazon S3
   │
   ▼
Image URL
   │
   ▼
Amazon RDS
   │
   ▼
Response
기술 스택
Backend
Spring Boot
Spring MVC
Spring Data JPA
Database
Amazon RDS (MySQL)
Cloud
Amazon EC2
Amazon S3
AWS SDK
S3Client
ConfigurationProperties
Architecture
REST API
DTO
Service Layer
GlobalExceptionHandler
JPA Auditing
주요 특징
Spring Boot 기반 쇼핑몰 백엔드 구현
MultipartFile 기반 이미지 업로드
Amazon S3 이미지 저장
Amazon EC2 서버 운영
Amazon RDS(MySQL) 연동
Spring Data JPA 기반 도메인 설계
DTO 기반 계층형 아키텍처
GlobalExceptionHandler 기반 예외 처리
환경변수 기반 AWS 인증 정보 관리
실무 환경을 고려한 AWS 백엔드 아키텍처 설계
기대 효과
AWS 클라우드 환경에서 이미지 업로드와 상품 관리 기능을 안정적으로 제공
S3, EC2, RDS를 연계한 백엔드 아키텍처를 통해 실제 서비스와 유사한 운영 환경을 경험
계층형 구조와 JPA 기반 설계를 적용하여 유지보수성과 확장성을 고려한 백엔드 시스템을 구축
환경변수 기반 인증 정보 관리와 예외 처리 체계를 적용하여 보안성과 안정성을 향상
