- MySQL 데이터베이스를 복수의 가용영역에 이중화로 구성하고 리눅스 기반의 가상 서버와 MySQL 데이터베이스를 연결
	- Amazon RDS 이용
- DB중 하나를 마스터로, 다른 하나를 Stand-by로 설정하게 된다.
	- 기본적으로는 Master와 서버와 연결되어 사용, 만약 마스터가 죽으면 Stand-by DB로 자동 연결이 된다.
		- 이때 서로 역할이 바뀌게 된다.
- 읽기 전용 Read Replica는 Master와 싱크 맞추면서 변동되는 것을 실시간으로 업데이트 할 수 있다.
- 어플리케이션 로드 밸런서를 이용해 웹서버가 사용자의 요청을 수신하면, 서버는 요청에 대한 응답을 NAT Gateway로 보낸다.
	- 이 과정에서 데이터베이스에서 가져와야 할 정보가 있는 경우 private 웹 서버를 거쳐 NAT로 응답을 유저에게 보내게 된다.
- 다음과 같은 과정으로 만들어질 수 있다.
	1. RDS용 Security Group 생성
	2. Subnet Group todtjd
	3. 복수의 가용 영역에 MySQL 데이터베이스 설정
		- DB Engine / Instance / Storage
		- Availability & Durability / Connectivity / Authentication / Backup 등을 설정한다.
	4. 데이터베이스 정보 확인
- 웹 서버와 데이터베이스는 다음과 같이 연결할 수 있다.
	1. EC2-RDB 연결을 위한 정보를 구성한다.
		- Endpoint / Master User / Master Password 등
	2. DB에 접속한다
	3. 테이블을 생성하고 데이터를 입력한다.
	4. 웹 브라우저를 통해 데이터베이스가 연결되었는지 테스트한다.
- DB의 Read Replica 생성을 다음과 같이 수행할 수 있다.
	1. DB Read Replica 생성
	2. EC2-Read Replica 데이터베이스 연결
	3. 웹 브라우저를 통해 DB 연결 테스트
	4. 원본 DB 변경 후 웹 브라우저를 통해 Read Replica 반영 테스트
- Failover를 이용한 DB 이중화 테스트는 다음과 같이 수행된다.
	1. Master / Standby DB의 IP 정보 확인
	2. Master DB Failover 테스트 -> Reboot를 이용
	3. Standby DB가 Master로 전환되었는지 확인
	4. 웹 브라우저를 통해 데이터베이스 연결 테스트