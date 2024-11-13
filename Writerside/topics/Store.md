# Store

인스턴스 스토어
- 블록 수준 스토리지 볼륨은 물리적 하드 드라이브처럼 동작
- 인스턴스에 임시 블록 수준 스토리지를 제공
- 인스턴스에 물리적으로 연결
- 인스턴스가 종료되면 데이터가 손실됨

AWS Elastic Block Store(EBS)
- 블록 수준 스토리지 볼륨 제공하는 서비스
- 인스턴스가 중지, 종료 되어도 연결된 EBS 볼륨의 모든 데이터 사용 가능
- EBS 볼륨 생성한 다음 인스턴스에 연결하면 된다.
- EBS는 보존해야하는 데이터를 위한 것, EBS 스냅샷을 생성하여 EBS 볼륨을 증분 백업 가능
- 단일 가용 영역에 데이터를 저장

EBS 스냅샷
- 증분 백업
- 처음 볼륨을 백업하면 모든 데이터가 복사 (전체 백업)
- 이후 백업은 변경된 데이터 블록만 저장 (증분 백업)

객체스토리지
- 각 객체는 데이터, 메타데이터, 키로 구성

S3
- 객체 수준 스토리지 제공 서비스
- 저장 공간을 무제한으로 제공, 객체의 최대 파일 크기는 5TB
- 파일을 업로드 할 때 권한을 설정하여 파일에 대한 표시 여부 및 액세스를 제어
- S3 버전 관리 기능을 사용하여 시간 경과에 따른 객체 변경 사항을 추적

S3 스토리지 클래스
- S3는 사용한 만큼만 비용을 지불
- 선택 고려 사항(데이터를 검색할 빈도, 필요한 데이터 가용성)
1.  Standard
    - 자주 액세스
    - 최소 3개의 가용 영역에 데이터를 저장 (고가용성)
2. Standard-Infrequent Access (IA)
    - 자주 액세스 하지 않음
    - 최소 3개의 가용 영역에 데이터를 저장 (고가용성)
    - 스탠다드보다 스토리지 가격은 저렴하나 검색 가격은 더 높음
3. One Zone-IA
    - 단일 가용 영역
    - IA 보다 낮은 스토리지 가격
4. Intelligent-Tiering
    - 엑세스 패던을 알수 없거나 자주 변화하는 데이터에 이상적
    - 객체당 소량의 월별 모니터링 및 자동화 요금을 부과
    - 30일 연속 미 액세스시 IA로 이동, 액세스시 Standard로 이동
5. Glacier Instant Retrieval
    - 즉각적인 액세스가 필요한 데이터에 적합
    - 몇 밀리초만에 객체 검색 가능
6. Glacier Flexible Retrieval
    - 데이터 보관용으로 설계된 저비용스토리지
    - 객체를 몇 분에서 몇 시간 이내에 검색
7. Glacier Deep Archive (가장 저렴!)
    - 가장 저렴한 객체 스토리지 클래스로 보관에 적합
    - 12시간 이내에 객체를 검색
8. Outposts
    - 온프레미스 Outposts 환경에 객체 스토리지를 제공

EBS vs S3
- 리전 별로 분산되어 있고, 백업 전략을 고민할 필요가 없을 때, S3를 선택 서버리스의 장점도 있다.
- 객체 데이터를 빈번하게 수정해야 할 때는 EBS 증분 백업 전략이 도움이 된다.

블록 스토리지 및 객체 스토리지와 비교하면 파일 스토리지는 많은 수의 서비스 및 리소스가 동시에 동일한 데이터에 액세스해야하는 사용 사례에 이상적

AWS Elastic File System (EPS)
- 클라우드 서비스 및 온프레미스 리소스와 함께 사용되는 확장 가능한 파일 시스템
- 파일을 추가 및 제거하면 자동으로 확장하거나 축소
- 애플리케이션을 중단하지 않고 온디맨드로 페타바이트 규모까지 확장 가능
- EC2에 EBS를 연결하려면 동일한 가용영역에 상주해야한다.
- EPS는 리전별 서비스여서 여러 가용영역에 걸쳐 데이터를 저장 된다.
  - 중복 스토리지를 사용하면 파일 시스템이 위치한 리전의 모든 가용영역에서 동시에 데이터에 액세스할 수 있다.
  - 온프레미스 서버는 AWS Direct Connect를 사용해 EFS에 액세스 할 수 있다.

AWS Relational Database Service (RDS)
- 클라우드에서 관계형 데이터베이스를 실행할 수 있는 서비스
- 하드웨어 프로비저닝, 데이터베이스 설정, 패치적용, 백업과 같은 작업 자동화하는 관리형 서비스
- 다른 서비스와 통합해 서버리스 애플리케이션에서 데이터베이스를 쿼리하는 등 비즈니스 및 운영 요구 사항을 충족
- 다양한 보안 옵션 제공 (DB이 저장시 암호화 및 전송 중 암호화 제공)
- Aurora, Pg, MySql, MariaDB, Oracle, SQL Server 지원
- Amazon Aurora
  - 엔터프라이즈급 관계형 데이터베이스
  - MySql, Pg 호환
  - MySql 보다 5배 빠르고, PG보다 3배 빠름
  - 리소스의 신뢰성 및 가용성을 유지하면서 불필요한 입출력 작업을 줄여 데이터베이스 비용 절감
  - 6개의 데이터 복사본을 3개의 가용 영역에 복제하고 지속적으로 S3에 데이터를 백업

AWS DynamoDB
- 키-값 데이터베이스 서비스
- 한 자릿수 밀리초의 성능을 제공
- 서버리스로 서버를 프로비저닝, 패치 적용 또는 관리할 필요가 없고, 소프트웨어를 설치, 유지관리 운영할 필요가 없다.
- 데이터베이스 크기가 축소 또는 확장되면 용량 변화에 맞춰 자동으로 크기 조정
- 일관된 성능을 유지
- 크기를 조정하는 동안에도 고성능이 필요한 사용 사례에 적합

AWS Redshift
- 빅데이터 분석에 사용할 수 있는 데이터 웨어하우징 서비스
- 데이터를 수집하여 데이터 간의 관계 및 추세를 파악하는데 도움이 되는 기능을 제공
- 확장성 제공
- Redshift Spectrum을 통해 데이터 레이크에서 실행되는 수 엑사바이트의 비정형 데이터를 대상으로 단일 SQL 쿼리 실행 가능
- 비즈니스 인텔리전스 워크로드에 대해 기존 데이터베이스 대비 최대 10배나 높은 성능을 제공

AWS Database Migration Service (DMS)
- 관계형, 비관계형 데이터베이스 및 기타 유형의 데이터 저장소를 마이그레이션 할 수 있는 서비스
- 원본과 대상 데이터베이스 간에 데이터를 이동할 수 있다.
- 원본과 대상 데이터베이스 유형이 동일할 필요는 없다.
- 마이그레이션 동안 원본 데이터베이스가 계속 작동하므로 가동 중지 시간을 줄일 수 있다.
- 사례) 개발 및 테스트 DB 마이그레이션, 데이터베이스 통합, 연속 복제

그외..
1. DocumentDB - MongoDB 워크로드를 지원하는 문서 데이터베이스 서비스
2. Neptune - 그래프 데이터베이스 서비스 (추천엔진, 사기행위탐지, 지식그래프 고도로 연결된 데이터 세트)
3. Quantum Ledger Database(QLDB) - 원장 데이터베이스 서비스, 데이터에 발생한 모든 변경 사항의 전체 기록을 검토
4. Managed Blockchain - 블록체인 네트워크를 생성하고 사용할 수 있는 서비스, 분산형 원장 시스템
5. ElastiCache - Redis 자주 사용되는 요청의 읽기 시간을 향상시키기 위해 데이터베이스 위에 캐싱 계층을 추가하는 서비스
6. DynamoDB Accelerator(DAX) - DynamoDB용 인메모리 캐시, 응답시간을 마이크로 초까지 향상