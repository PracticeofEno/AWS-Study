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
