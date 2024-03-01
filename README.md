# Deploy_Test

### AWS S3 와 CloudFront를 사용하여 React App 배포 연습하기

### S3 (Simple Storage Service)
확장성, 데이터 가용성 및 보안과 성능이 우수한 객체 스토리지 서비스

### CloudFront 
콘텐츠 전송 네트워크(CDN) 서비스로, 사용자가 웹 사이트 및 애플리케이션을 더 빠르게 로드할 수 있도록 도와줌 

*** 

### S3와 CloudFront를 연동할 때의 이점

#### 1. 콘텐츠 캐싱을 통한 S3 부하 감소
  - 전 세계에 분산된 Edge Location에 콘텐츠를 캐싱하고, 사용자가 요청한 콘텐츠가 해당 Edge Location에 이미 캐시되어 있다면, 즉시 콘텐츠를 제공함
#### 2. Edge Location을 통한 응답속도 향상
  - 사용자의 디바이스에서 가장 가까운 Edge Location에서 콘텐츠를 다운받기 때문에 네트워크 지연이 최소화되어 웹사이트나 애플리케이션 성능이 향상됨

#### 3. 콘텐츠 보안 유지
  - SSL/TLS를 통한 데이터 암호화 및 사용자 인증, 접근 제어를 제공하며 AWS WAF와 통합하여 웸 애플리케이션 방화벽을 통해 보안을 강화할 수 있음
***

## 실제 배포 예시

### 실제 S3 버킷 주소를 입력하여 접근 시 403 에러 발생 

<img width="800" alt="스크린샷 2024-03-01 오후 9 44 33" src="https://github.com/Lee-Dongwook/FE_Deploy_Test/assets/97590636/047c4b9a-5942-4820-9b84-52b3e16ef499">

*** 

### CloudFront에서 제공하는 도메인 주소 연결 시 정상 접속 가능

<img width="800" alt="스크린샷 2024-03-01 오후 9 43 14" src="https://github.com/Lee-Dongwook/FE_Deploy_Test/assets/97590636/2163cc9c-b05f-4abf-bdc9-dd16c3e90afc">
