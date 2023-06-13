# 2023 Cloud Security Guideline
[1. AWS SSB에 따른 보안 진단 가이드라인 문서](https://github.com/ottlseo/2023-Cloud-Security-Guideline/edit/main/README.md#1-aws-ssb%EC%97%90-%EB%94%B0%EB%A5%B8-%EB%B3%B4%EC%95%88-%EC%A7%84%EB%8B%A8-%EA%B0%80%EC%9D%B4%EB%93%9C%EB%9D%BC%EC%9D%B8-%EB%AC%B8%EC%84%9C)   
[2. 보안 진단 애플리케이션 실행 방법](https://github.com/ottlseo/2023-Cloud-Security-Guideline/edit/main/README.md#2-%EB%B3%B4%EC%95%88-%EC%A7%84%EB%8B%A8-%EC%95%A0%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EC%8B%A4%ED%96%89-%EB%B0%A9%EB%B2%95)

- - -

## 1. AWS SSB에 따른 보안 진단 가이드라인 문서
AWS Startup Security Baseline을 참고하여, 개발자들이 실질적으로 AWS 내 클라우드 보안을 체크하고 보완할 수 있는 형태의 가이드라인을 제공합니다.    
해당 가이드라인은 무료 배포되어, 누구나 접근해 읽어볼 수 있고 Comment 기능을 이용해 피드백을 남길 수 있습니다. 

#### 👉 [가이드라인 바로 가기 (Notion)](https://yoonseo.notion.site/2023-Cloud-Security-Guideline-2efe010bacb442279dbf5a30e4150a77)

#### 1. Account 및 IAM 설정

이 항목에서는 계정 정보와 루트 계정을 포함한 IAM 설정에 대하여 진단합니다.

- 대체 연락처 정보가 기입되어 있는지
- 루트 유저에 MFA 설정 등의 설정이 되어있는지
- IAM User를 사용하는지
- IAM User에 직접 권한을 할당하여 사용하는지

#### 2. CloudTrail 설정

이 항목에서는 아래 CloudTrail 설정에 대하여 진단합니다.

- CloudTrail이 켜져 있는지
- CloudTrail이 multi-region으로 되어있는지

#### 3. S3 설정

이 항목에서는 S3 버킷의 퍼블릭 엑세스 정책에 대하여 진단합니다.

- 계정의 S3 퍼블릭 엑세스 정책이 차단되어있는지
- 개별 S3 버킷의 퍼블릭 엑세스가 차단되어있는지

#### 4. 기타 설정

이 항목에서는 나머지 AWS SSB 항목에 대하여 진단합니다.

- VPC, Subnet, Securit Group 체크
- 비용 및 루트 계정 엑세스 알람 설정
- Trusted Advisor 기능
- GuardDuty 기능

위 과정을 통해 진단된 결과는 HTML 형식의 리포트로 s3 버킷에 저장됩니다.

#### 참고 자료
- [AWS Startup Security Baseline](https://docs.aws.amazon.com/prescriptive-guidance/latest/aws-startup-security-baseline/welcome.html)
- [AWS Shared Responsibility Model](https://aws.amazon.com/ko/compliance/shared-responsibility-model/?nc1=h_ls)

- - - 

## 2. 보안 진단 애플리케이션 실행 방법
해당 애플리케이션을 실행하는 데에 SAM(Serverless Application Model) CLI 설치가 필요합니다.
로컬 터미널에 SAM CLI를 Download 하거나, AWS Cloud9 터미널을 이용해주세요.

1. 터미널을 열고 아래 명령어를 입력하여, 해당 Repository를 Clone 하고 디렉토리로 들어갑니다:

```
git clone https://github.com/ottlseo/2023-Cloud-Security-Guideline
cd 2023-Cloud-Security-Guideline
```
2. 터미널에 아래 명령어를 입력합니다. AWS SAM을 이용하여 template.yaml파일에 정의된 리소스를 배포하는 과정입니다:

```
sam deploy --guided
```
3. Prompt에 아래와 같은 입력값이 요구됩니다. 본인의 환경에 맞춰 입력해주세요:
```
stack name: ssb-app (또는 본인이 원하는 스택 이름을 입력 가능합니다)
desired AWS Region: ap-northeast-1 (또는 원하는 AWS 리전을 입력 가능합니다)
이후 SAM CLI, IAM role과 관련된 옵션에는 Y/N 으로 입력해주세요.(Enter를 입력해서 default setting을 설정하실 수 있습니다.)
```

4. 이후 스택이 배포되며, 입력한 이메일로 SNS Topic 구독을 요청하는 이메일이 발송됩니다. 메일의 Confirm subscrption을 클릭하여 먼저 알림을 구독해주세요. 

![image](https://github.com/ottlseo/2023-Cloud-Security-Guideline/assets/61778930/040a5e73-2e75-40c9-b390-9bde3be4eb32)

5. AWS Step Functions 콘솔로 이동하여, 생성된 상태머신을 실행 시작 버튼을 눌러 실행합니다. 
6. 이후 상태머신이 아래와 같이 실행되며, SNS 구독을 한 이메일로 리포트를 다운로드할 수 있는 URL이 발송됩니다. 

7. URL에 접근하여 아래와 같은 리포트를 확인하실 수 있습니다. 

<img width="720" alt="image" src="https://github.com/ottlseo/2023-Cloud-Security-Guideline/assets/61778930/c86de475-965a-49d7-906b-c9cf7ba26897">

