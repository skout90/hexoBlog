IDE

- AWS Cloud9



기계 학습

- SageMaker



Haddop

HDFS / EMR



ML.AWS 방문하면 머신러닝 정보 얻을 수 있음.



## AWS SAM 서버리스

- AWS CodeCommit - AWS CodeBuild - AWS Code Deploy

  위 과정을 AWS CodePipeline을 통해 진행

  > 또는 Code Start / Cloud9을 이용

- AWS CodeStart : 데브 옵스를 위한 손쉬운 프로젝트 운영 -> 위 과정을 추상화하여 제공

API Gateway

- AWS Cloud9 : 클라우드 기반 IDE/디버깅 손쉬운 개발



## 마이크로 서비스

- 컨테이너 스케줄링/스케일링 배포전략

EC2/EKS 

- 호스팅

EC2 / Fargate

- 컨테이너 이미지 저장소

ECR



ECS : Elastic Container Service



## CI / CD

하루에 여러번 코드를 커밋하고 병합하는것

- 작은 범위의 코드

CD는 개발자의 승인 필요 없이 자동 운영 환경 배포 : 코드가 테스트를 통과하기만 하면.



빌드/배포/테스트 단계 자동화!

릴리스 주기 가속화

개발자들이 빠르게 피드백 얻을 수 있음



향상된 협업

신속한 전달

신뢰성

보안

확장성



### 소스

코드 레파지토리 : 버전관리 / 브랜칭 / 코드리뷰

(코드 커밋) : 다른 서비스와 연동 가능

GitHub/BitBucket

### 빌드

컴파일 / 유닛테스트 / 정적 분석 / 패키징

(코드 빌드) : 컴파일 / 테스트 / 배포 준비 asset / VPC 액세스

(젠킨스)

### 테스트

통합 테스트 / 부하 테스트 / 보안 테스트 / 적용 테스트

### 배포

(코드 디플로이) : 배포를 자동화

다양한 배포 기법 : Rolling, Blue/Green, Canary



CI CD : CloudFormation 템플릿 작성 

![1531983286027](/tmp/1531983286027.png)



- Rolling 배포

일부 인스턴스부터 구 버전에서 새 버전으로 점진적으로 옮겨가게 됌.

- Canary

새 버전의 어플리케이션으로 프로덕션 트래픽의 일부를 분산

A / B 테스팅 사용 가능 

운영 환경 대체 / 중지 가능

![1531983773112](/tmp/1531983773112.png)





![1531984094582](/tmp/1531984094582.png)



## 영상 인식

- Amazon Kinesis Video Streams

이미지 또는 비디오를 Rekognition API에 제공하기만 하면, 서비스에서 객체, 사람, 텍스트, 장면 및 동작을 식별하고 부적절한 콘텐츠를 탐지할 수 있습니다. 또한, Amazon Rekognition은 여러분이 제공하는 이미지와 비디오에서 매우 정확한 얼굴 분석 및 얼굴 인식을 제공합니다. 사용자 확인, 인원 계산 및 공공 안전 등 다양한 사용 사례에서 얼굴을 탐지, 분석 및 비교할 수 있습니다













성공적인 SaaS 기업들의 4가지 비밀 

챗봇과 대화 인터페이스로 한 층 업그레이드 된 고객 경험