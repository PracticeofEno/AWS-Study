# AWS-study
## 출처 : https://explore.skillbuilder.aws/ 

## AWS Cloud Practitioner Essentials (Korean) (한국어 강의)

### 가상화
- 하이퍼바이저 :EC2간을 분리하고 리소스를 공유하는 책임을 담당
- 멀티테넌시 : 가상컴퓨터간 기본 하드웨어 공유 
- 수직 확장 : 서비스를 제공하다 리소스가 더 필요하면 별도의 처리 없이 설정만 바꿔주면 됨
- EC2의 네트워크 제어가능
- 서비스로서의 컴퓨팅(Caas)

### Amazon EC2 인스턴스 유형
- 각 Amazon EC2 인스턴스 유형은 인스턴스 패밀리로 그룹화
- 범용, 컴퓨팅 최적화, 메모리 최적화, 액셀러레이티드 컴퓨팅, 스토리지 최적화 
- 범용 : 균형잡힌
- 컴퓨팅 : 고성능 프로세서를 활용해야하는 컴퓨팅 집약적인 애플리케이션 작업
- 메모리 : 대규모 데이터 세트를 처리하는 작업
- 엑셀러레이티드 : 하드웨어 액셀러레이터 or 코프로세서를 사용하여 일부 기능을 CPU에서 실행되는 소프트웨어에서보다 더 효율적으로 수행 (ex. 그래픽 애플리케이션)
- 스토리지 : 로컬 스토리지의 대규모 데이터 세트에 대한 순차 읽기 및 액세스가 많이 필요할때

### Amazon EC2 구매 옵션
- 온디맨드 : 사용한 만큼
- Savings Plans: 일정한 사용량을 약정하는 대가로 일정 용량만큼 할인.
- 예약 인스턴스 : 사용량이 예측 가능한 워크로드에 적합
- 스팟 인스턴스 : AWS가 필요시에 언제든 인스턴스 용량을 회수할 수 있음, 회수2분전에 경보가 제공, 배치워크로드에 적합
- 전용 호스트 : EC2가 사용하는 물리적 호스트를 전용으로 사용할 수 있게 해줌.

### Amazon EC2 Auto Scaling
- Auto Scaling 그룹에서 최소, 희망, 최대 용량 설정가능 (설정 하지 않으면 희망은 최소용량으로 설정)
#### 조정 방법
- 동적 조정 : 수요 변화에 대응
- 예측 조정 : 예측된 수요에 따라 적절한 수의 EC2 인스턴스를 자동으로 예약
#### 확장 방법
- 수직 확장 : CPU를 좋은 설정으로
- 수평 확장 : 인스턴스(ex.EC2)를 하나 더 

※동적 조정과 예측 조정을 함께 사용하면 더 빠르게 조정할 수 있습니다.

### Elastic Load Balancing 
- 리전 수준 구조 : EC2가 아닌 리전 수준에서 실행됨으로 사용자가 추가적으로 작업하지 않아도 자동으로 고가용성으로 확장 
- 외부에서만 사용되는게 아니고 FrontEnd EC2와 Backend EC2 사이에도 위치함
<img src="https://user-images.githubusercontent.com/57505385/215297634-e98f4395-c88b-4b27-b537-55bf2d1d57e8.png" width="40%"> to <img src="https://user-images.githubusercontent.com/57505385/215297666-1a267cae-4e44-490d-94c5-36ad185d127c.png" width="40%">
example)
[요청] <- ELB -> [EC2]
요청이 많아지면 EC2를 만들고 EC2가 Online이 되면 ELB에 메세지를 날려 처리를 시작
요청이 적어지면 EC2에 남은 처리를 다 끝낸뒤 종료함

### 메시징 및 대기열
- 밀결합된 애플리케이션 : 하나의 장애가 다른곳의 장애를 일으키는 아키텍처
<img src="https://user-images.githubusercontent.com/57505385/215297943-1ae9ec77-8ab6-4b25-922c-6f6af46640aa.png" width="40%">
- 소결합된 애플리케이션 : 하나의 장애가 발생해도 다른곳으로 장애가 퍼지지 않는 아키텍처
<img src="https://user-images.githubusercontent.com/57505385/215297963-cda315ef-bcca-4dbe-847f-58c1df8b0f2e.png" width="40%">

#### Amazon Simple Notification Service(Amazon SNS)
Amazon Simple Notification Service(Amazon SNS)는 게시/구독 서비스입니다. 
게시자는 Amazon SNS 주제를 사용하여 구독자에게 메시지를 게시합니다. 
이는 커피숍에서 계산원이 음료를 만드는 바리스타에게 주문 사항을 전달하는 것과 비슷합니다.
Amazon SNS에서 구독자는 웹 서버, 이메일 주소, AWS Lambda 함수 또는 그 밖의 여러 옵션이 될 수 있습니다. 

### 추가 컴퓨팅 서비스
- 서버리스 : 기본 인프라를 보거나 액세스 할 수 없음

#### AWS Lambda 
- 서버리스 컴퓨팅 옵션의 대표적인 서비스
- 사용자가 코드를 Lambda 함수라는 곳에 업로드 할수있게 도와주는 서비스
- 서비스가 트리거를 기다리다 감지되면 관리형 환경에서 자동으로 실행이 됨.
- 실행 시간이 15분 미만이여야 함
- 15분이 걸리지 않는 빠른 처리에 적합
- 코드를 실행하는 동안에만 요금이 부과됨

#### Amazon Elastic Container Service (ECS), Amazon Elastic Kubernetes Service (EKS)
- 컨테이너(도커) 오케스트레이션 도구 
- 운영체제수준에서의 가상화를 제공
- 이 경우 EC2에서 실행할 수 있음

-> 기본적인 OS에 액세스할 필요 없거나 EC2 를 컨트롤 하지 않아도 되는 경우는 AWS Fargate 를 사용하는게 좋음
#### AWS Fargate 
- AWS Fargate는 컨테이너용 서버리스 컴퓨팅 엔진으로, Amazon ECS와 Amazon EKS에서 작동
- AWS Fargate를 사용하는 경우 서버를 프로비저닝하거나 관리할 필요가 없음
- AWS Fargate는 자동으로 서버 인프라를 관리
- 컨테이너를 실행하는 데 필요한 리소스에 대해서만 비용을 지불하면 됩니다.


### AWS 리소스를 프로비저닝 하는방법
1. AWS manage console -> GUI(수동)
2. AWS CLI -> 스크립팅 가능 
3. AWS SDK -> 개발자 도구를 통해서 프로그래밍형태로
4. AWS Elastic Beanstalk -> 사용자가 코드 및 구성 설정을 제공하면 Elastic Beanstalk이 다음 작업을 수행하는 데 필요한 리소스를 배포
5. AWS CloudFormation ->  코드 줄을 작성하여 환경을 구축할 수 있음 (ex. json / yaml)

### 네트워킹
- Amazon VPC를 이용하여 가상 네트워크 리소스를 구축 가능.
- 인터넷 게이트웨이를 사용해서 open 가능  
<img src="https://user-images.githubusercontent.com/57505385/215354250-d4eb184e-c7d0-4f3f-adb3-46e5aeb90a4c.png" width="60%">
- 가상 프라이빗 게이트웨이 : 특정 경로만 허용하고 다 차단한 상태(트래픽 통로는 공유함)
<img src="https://user-images.githubusercontent.com/57505385/215354276-bf17f30f-f2cd-4d9b-badc-acd895e045f0.png" width="60%">
- Amazon Direct Connect : 직접 회선 따서 연결
<img src="https://user-images.githubusercontent.com/57505385/215354429-23fee190-ced5-4dd5-acc5-788277986dbd.png" width="60%">
- 서브넷 : 서브넷은 보안 또는 운영 요구 사항에 따라 리소스를 그룹화할 수 있는 VPC 내의 한 섹션입니다. 서브넷은 퍼블릭 또는 프라이빗일 수 있습니다.
<img src="https://user-images.githubusercontent.com/57505385/215354875-5673330e-328a-4e0f-956d-8dd047c9a47c.png" width="60%">
- 네트워크 ACL(액세스 제어 목록) : 네트워크 ACL(액세스 제어 목록)은 서브넷 수준에서 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽
- 보안 그룹 : Amazon EC2 인스턴스에 대한 인바운드 및 아웃바운드 트래픽을 제어하는 가상 방화벽
- 총 구성 
<img src="https://user-images.githubusercontent.com/57505385/215354991-fea84b77-d2dd-47cc-90fd-cc9c43cac17c.png" width="60%">


### 스토리지 및 데이터베이스
- 블록 수준 스토리지 : SSD, 하드디스크 같은 자주 변경되는 데이터유형
- EC2를 실행하면 인스턴스 스토리지 볼륨이라는 곳에 기본적으로 저장됨 -> 중단하면 스토리지가 날아감(휘발성)

#### Amazon Elastic Block Store (EBS)
1. 재시작해도 안날아감 따로 저장됨
2. 크기, 유형, 구성을 정의하고 프로비저닝함
3. 스냅샷 이라고 하는 증분 백업을 만들 수 있음. ★
<img src="https://user-images.githubusercontent.com/57505385/215355785-faa86b81-34fe-447a-8960-395a3ba1d42e.png" width="60%">

#### Amasozn Simple Storage Service (S3)
- 데이터를 객체로 저장 ★
- 일부 객체가 변경될때마다 전체 파일을 다시 업데이트 ★
- 객체를 버킷(파일디렉토리같은)에 저장
- 최대 5TB크기의 객체를 업로드
- 객체 버전 관리
- 여러 버킷 생성(자주 접속 or 장기간 보관)
- 정적 웹사이트 호스팅 가능 
- 리전별 분산 (99.999999% 안전, 그냥 안전)
- S3 Standard-IA : 액세스 빈도는 낮지만 필요할 경우 빠르게 액세스 해야하는 경우(백업,재해복구 파일 등)
- Amazon S3 Glacier : S3를 글래시어로 저장가능. 데이터 유지기간 같은, 정책으로 읽고쓰기 제어 가능, 한번 잠금하면 변경 불가
- Amazon S3 수명주기 설정 : 일정 시간이 지나면 계층 사이에서 데이터를 자동으로 이동

#### Amazon Elastic File Stytem(EFS)
- 여러 인스턴스가 동시에 EFS의 데이터에 액세스 가능
- EFS -> Linux 파일 시스템, 리전 영역 리소스(리전은 여러개의 가용영역), 자동 확장
- EBS와 다른점 -> EBS는 인스턴스에 볼륨연결, 가용영역 수준의 리소스, EC2인스턴스를 연결하려면 동일한 가용영역에 있어야 함, 볼륨이 자동으로 확장되지 않음

#### Amazon Relational Database Service(Amazon RDS)
- 리프트 앤 시프트 마이그레이션 : 온프레미스 환경에서 클라우드로 
- 자동패치, 백업, 이중화 , 장애조치, 재해 복구
- Amazon Aurora :엔터프라이즈급 관계형 데이터베이스. 이 데이터베이스는 MySQL 및 PostgreSQL 관계형 데이터베이스와 호환. 표준 MySQL 데이터베이스보다 최대 5배 빠르며 표준 PostgreSQL 데이터베이스보다 최대 3배 빠름, 데이터를 가용영역에 복제해서 안전하며 S3에 지속적으로 백업

#### Amazon Dynamo DB (NoSQL 데이터베이스 서비스인듯)
- 비관계형 데이터베이스
- NoSQL의 특성을 지님
- 서버리스 데이터 베이스

#### Amazon Refshift : 빅데이터 vI솔루션이 필요할때 단일 API호출로 실행할 수 있다는것
#### AWS Database <igration Service (amazon DMS)
- 기존 데이터베이스를 안전하고 쉽게 AWS로 마이그레이션 할수있음
- 마이그레이션이 진행되는 동안 소스 데이터베이스의 모든 기능이 정상 동작
- 원본 데이터베이스와 대상 데이터베이스의 유형이 동일하지 않아도 됨.
- 개발 및 테스트 데이터베이스 마이그레이션
- 데이터베이스 통합
- 연속 복제 등에 사용
- 동종 데이터베이스 (동종 마이그레이션)
: 스키마구조, 데이터유형, 데이터베이스 코드가 호환됨.
: 온프레이스 or EC2 or REDS  -> Amazon EC2, Amazon blabla
- 이종 데이터베이스 (이종 마이그레이션)
1단계 : 스키마구조, 데이터유형, 데이터베이스 코드가 다름 -> Amazon Scheama Convertsion 실행 -> 스키마구조, 데이터베이스 코드 가 변환
2단계 : DMS를 사용하여 마이그레이션

### 보안
#### IAM : Identity Acess Management 
- AWS 서비스와 리소스에 대한 액세스를 안전하게 관리
- IAM 사용자, 그룹 및 역할
- IAM 정책
- Multi-Factor Authentication
example)
<img src="https://user-images.githubusercontent.com/57505385/215361066-8b7bf82c-d512-48f6-af67-24e500dce9a4.png" width="40%">

