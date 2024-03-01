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

## 과정

### 1. S3 버킷을 생성한다.
- ### 1-1. 객체 소유권 - ACL(엑세스 제어 목록)을 활성화하고, 객체 라이터가 객체 소유자로 유지되도록 설정
- ### 1-2. 버킷의 퍼블릭 엑세스 차단 설정을 모두 해제하여 객체를 퍼블릭 상태로 만든다.
- ### 1-3. [속성] 탭의 정적 웹 사이트 호스팅을 활성화 한다.
- ### 1-4. 버킷 정책의 권한을 다음과 같이 지정한다.
  ```json
    {
	    "Version": "2012-10-17",
	    "Statement": [
		    {
			    "Sid": "Statement1",
			    "Principal": "*",
			    "Effect": "Allow",
			    "Action": [
				    "s3:GetObject"
			    ],
			    "Resource": [
				    "arn:aws:s3:::<버킷이름>/*"
			    ]
		    }
	    ]
    }
  ```

### 2. CloudFront를 배포한다.
- ### 2-1. 원본 도메인을 지정하고, 원본 엑세스 제어 설정을 하여 OAC(Origin Access Control)을 설정한다.
- ### 2-2. 기본 캐시 동작의 뷰어 프로토콜 정책, HTTP 허용 정책, 캐시 키 및 원본 요청 등을 설정한다.
- ### 2-3. 웹 애플리케이션 방화벽(WAF) 설정을 한다.
- ### 2-4. CNAME, SSL 인증서, 기본값 루트 객체 등을 설정하고 배포를 생성한다.
- ### 2-5. S3 버킷 정책의 권한을 다음으로 수정한다.
```json
{
        "Version": "2008-10-17",
        "Id": "PolicyForCloudFrontPrivateContent",
        "Statement": [
            {
                "Sid": "AllowCloudFrontServicePrincipal",
                "Effect": "Allow",
                "Principal": {
                    "Service": "cloudfront.amazonaws.com"
                },
                "Action": "s3:GetObject",
                "Resource": "arn:aws:s3:::<버킷이름>/*",
                "Condition": {
                    "StringEquals": {
                      "AWS:SourceArn": "arn:aws:cloudfront::<계정id>:distribution/<배포id>"
                    }
                }
            }
        ]
      }
```

*** 


## 실제 배포 예시

### 실제 S3 버킷 주소를 입력하여 접근 시 403 에러 발생 

<img width="800" alt="스크린샷 2024-03-01 오후 9 44 33" src="https://github.com/Lee-Dongwook/FE_Deploy_Test/assets/97590636/047c4b9a-5942-4820-9b84-52b3e16ef499">

*** 

### CloudFront에서 제공하는 도메인 주소 연결 시 정상 접속 가능

<img width="800" alt="스크린샷 2024-03-01 오후 9 43 14" src="https://github.com/Lee-Dongwook/FE_Deploy_Test/assets/97590636/2163cc9c-b05f-4abf-bdc9-dd16c3e90afc">
