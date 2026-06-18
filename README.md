# AWS SDK Study

Java · Spring Boot · AWS S3 기반 클라우드 파일 업로드를 단계별로 학습한 실습 저장소입니다.

---

## 기술 스택

![Java](https://img.shields.io/badge/Java_17-007396?style=flat&logo=openjdk&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot_3.4-6DB33F?style=flat&logo=springboot&logoColor=white)
![AWS S3](https://img.shields.io/badge/AWS_S3-FF9900?style=flat&logo=amazons3&logoColor=white)
![AWS SDK](https://img.shields.io/badge/AWS_SDK_v2-232F3E?style=flat&logo=amazonaws&logoColor=white)
![Spring Cloud AWS](https://img.shields.io/badge/Spring_Cloud_AWS-6DB33F?style=flat&logo=spring&logoColor=white)
![Thymeleaf](https://img.shields.io/badge/Thymeleaf-005F0F?style=flat&logo=thymeleaf&logoColor=white)
![Lombok](https://img.shields.io/badge/Lombok-BC0000?style=flat&logoColor=white)
![Gradle](https://img.shields.io/badge/Gradle-02303A?style=flat&logo=gradle&logoColor=white)

---

## 프로젝트 구조

```
aws-sdk/
└── src/main/
    ├── java/com/example/demoawssdk/
    │   ├── DemoAwsSdkApplication.java   # 진입점
    │   ├── AwsS3Config.java             # AmazonS3 Bean 구성 (accessKey, secretKey, region)
    │   ├── controller/
    │   │   ├── HomeController.java      # 업로드 페이지 렌더링 (GET /upload)
    │   │   └── AwsS3Controller.java     # REST API — 파일 업로드 (POST /api/s3/upload)
    │   ├── dto/
    │   │   └── ResDto.java              # 응답 DTO (S3 퍼블릭 URL)
    │   └── service/
    │       └── AwsS3Service.java        # S3 업로드 핵심 로직
    └── resources/
        └── templates/
            └── upload.html              # 파일 업로드 UI (Fetch API 비동기 처리)
```

---

## 실행 방법

```bash
# 1. IntelliJ → File > Open → aws-sdk 선택
# 2. build.gradle 인식 후 의존성 다운로드 대기
# 3. application.properties에 AWS 접속 정보 설정
# 4. DemoAwsSdkApplication.java 실행
# 5. http://localhost:8080/upload 접속
```

`src/main/resources/application.properties`에 아래 값을 환경에 맞게 입력하세요.

```properties
cloud.aws.credentials.accessKey=YOUR_ACCESS_KEY
cloud.aws.credentials.secretKey=YOUR_SECRET_KEY
cloud.aws.region.static=ap-northeast-2
cloud.aws.s3.bucketName=YOUR_BUCKET_NAME
cloud.aws.stack.auto=false
```

> AWS IAM에서 S3 접근 권한이 있는 사용자의 액세스 키를 사용하세요.  
> 버킷 정책에서 퍼블릭 읽기 허용 여부를 확인하세요.

---

## 학습 내용

| 파일 | 주요 학습 내용 |
|------|---------------|
| `AwsS3Config.java` | `BasicAWSCredentials`로 인증 정보 구성, `AmazonS3ClientBuilder`로 S3 클라이언트 Bean 생성 |
| `AwsS3Service.java` | `PutObjectRequest` S3 업로드, UUID 기반 파일명 변조(중복 방지), `ByteArrayInputStream` 스트림 처리, MIME 타입(ContentType) 메타데이터 설정, 퍼블릭 URL 반환(`getUrl`) |
| `AwsS3Controller.java` | `MultipartFile` 수신, REST API 응답 구성 (`ResDto`) |
| `upload.html` | Fetch API 비동기 파일 업로드, `FormData` 구성, 업로드 결과 URL 표시 |

---

## 개발 환경

- **JDK 17** 이상 — [다운로드](https://download.oracle.com/java/17/archive/jdk-17.0.12_windows-x64_bin.exe)
- **IntelliJ IDEA** Ultimate (추천) / Community
- **AWS 계정** — S3 버킷 생성 및 IAM 액세스 키 발급 필요
