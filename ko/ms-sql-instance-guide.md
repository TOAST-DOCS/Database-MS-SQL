## Database > MS-SQL Instance > 사용 가이드

## MS-SQL 이미지 생성 후 초기 설정
### 1. SQL 인증모드 설정 
기본 인증 모드가 "Windows 인증 모드"로 되어 있습니다. 
MS-SQL의 DB 계정을 사용하기 위해 SQL 인증 모드로 변경이 필요합니다. 

서버 속성의 보안에서 서버 인증을 "SQL Server 및 Windows 인증 모드"으로 변경합니다.
!http://static.toastoven.net/prod_ms_sql/2275955677822839836.png
※ SQL 인증모드 설정후 적용을 위해 MS-SQL 서비스를 재시작해야 됩니다. 

### 2. MS-SQL 서비스 포트 변경 
MS-SQL의 기본 서비스 포트 1433은 널리 알려진 포트로 보안 취약점이 될 수 있습니다.
다른 포트로 변경하는것을 추천합니다. 

SQL Server 구성관리자의 SQL Server 구성관리자(로컬) > SQL Server 네트워크 구성 > MSSQLSERVER에 대한 프로토콜 > TCP/IP 의 속성에서 MS-SQL 서비스 포트를 변경합니다.
![image.png](/files/2275961179348076215)

TCP/IP 속성 > IPALL > TCP Port에 설정된 1433를 변경하고자하는 포트로 변경합니다.
![image.png](/files/2275962828638922719)

※ MS-SQL 서비스 포트 변경후 적용을 위해 MS-SQL 서비스를 재시작해야 됩니다. 

## 데이터 볼륨 할당
MS-SQL의 데이터/로그 파일(MDF/LDF), 백업 파일은 별도의 Block Storage 사용을 권장합니다. 
Block Storage 생성시 Volume 타입은 성능을 위해 "범용 SSD"를 추천합니다.

Block Storage 로 생성한 MS-SQL의 데이터 볼륨은 "컴퓨터 관리"의 컴퓨터 관리(로컬) > 저장소 > 디스크 관리에서 디스크 초기화, 볼륨 생성/할당/포멧을 진행합니다.
![image.png](/files/2276036582055744961)

서버 속성의 데이터베이스 설정에서 데이터베이스 기본 위치를 생성한 볼륨의 디렉토리로 변경합니다.
![image.png](/files/2276042525424064867)

※ MS-SQL 데이터베이스 기본 위치 변경후 적용을 위해 MS-SQL 서비스를 재시작해야 됩니다. 

## MS-SQL 서비스 재시작
MS-SQL의 설정 변경시 MS-SQL 서비스의 재시작이 필요한 경우가 있습니다.
변경 설정을 적용하기위해 MS-SQL을 재시작 합니다. 

SQL Server 구성관리자의 SQL Server 구성관리자(로컬) > SQL Server 서비스 > SQL Server(MSSQLSERVER)를 선택후 우클릭후 노출되는 메뉴에서 "다시 시작"으로 MS-SQL 서비스를 재시작합니다.
![image.png](/files/2275964667240225332)

## MS-SQL 서비스 자동 실행 확인/설정
MS-SQL의 서비스가 OS 구동시 자동으로 시작하도록 설정되어 있는지 확인합니다. 

SQL Server 구성관리자의  SQL Server 구성관리자(로컬) > SQL Server 서비스 에서 "시작모드"를 확인할 수 있습니다. 
![image.png](/files/2275967052178724395)

SQL Server (MSSQLSERVER), SQL Server 에이전트 (MSSQLSERVER) 등의 서비스의 시작 모드가 "자동"이 아닐 경우 해당 서비스를 선택하여 우클릭후 노출되는 메뉴의 "속성"을 실행하여 시작 모드를 변경합니다.
![image.png](/files/2275968204493195031)

속성창의 서비스탭에서 시작 모드를 자동으로 변경합니다. 
![image.png](/files/2275968334918331199)