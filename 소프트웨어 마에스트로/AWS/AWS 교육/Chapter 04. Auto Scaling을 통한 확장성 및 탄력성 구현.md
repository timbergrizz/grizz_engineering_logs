- AWS의 Auto Scaling 기능을 사용해 가상 서버의 용량을 자동으로 증가 / 축소하는 기능을 사용하여 인프라에 확장성과 탄력성을 구현한다.
	- 대부분의 Cloud Platform이 지원한다.
	- 클라우드 컴퓨팅의 가장 큰 장점이자, 사용하는 이유 중 하나.
- 서버에 설정한 값에 따라 규모를 조정해서 안정적으로 시스템을 구성하는 기능
	- 오토 스케일링 설정에 따라서 서버의 capacity가 증가하게 되는데, 이러한 상황을 scale out이라 한다.
		- scale out이 되더라도 각 private server에 있는 웹서버들은 어플리케이션을 통해 사용자의 요청을 수신하고, DB로 추가하여 NAT로 보내는 과정은 동일하다.
- Auto Scaling을 위한 Launch Template 및 Application Load Balancer 구성
	1. Private subnet의 EC2에 대한 Custom AMI를 생성한다.
	2. Auto Scaling을 위한 Launch Template 생성
		- AMI / Key Pair / Network / Storage 등
	3. Auto Scailing용 Application Load Balancer 구성 + 타겟 그룹
- Auto Scaling Group 및 Scaling Policy 구성
	1. Auto Scailing Group 생성
		- Launch Option / Group Size / Load Balancer / Tags 등
	2. Scaling Poilcy 구성
	3. 콘솔 및 웹 브라우저를 통해 Auto Scaling Group 시작 확인
- Auto Scaling Scale-Out 테스트
	1. Apache Bench Test를 위한 패키지 (httpd-tools) 설치
	2. Application Load Balancer에 부하(로드) 테스트
	3. CloudWatch를 통해 CPU Utilization rate 증가 확인
	4. Scale-out으로 EC2 증가 확인
- Auto Scaling Scale-in 및 Termination Policy 살펴보기
	- Scale-In으로 EC2 감소 확인
	- Auto Scaling Group의 Termination Policy 확인
