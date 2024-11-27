### Oracle 설치하기

-   설치 파일 다운로드
    -   [https://www.oracle.com/kr/downloads/](https://www.oracle.com/kr/downloads/)
    -   데이터베이스 > Database Express Edition > Oracle Database 21c Express Edition for Windows x64
    -   설치 중 패스워드 입력창이 나오면 패스워드 잊어버리지 않게 메모

<br>

### SQL Developer 설치하기

-   실행 파일 다운로드
    -   [https://www.oracle.com/kr/downloads/](https://www.oracle.com/kr/downloads/)
    -   개발자 툴 > SQL Developer > Windows 64-bit with JDK 8 included
    -   실행 파일이므로 별도의 설치 필요없음

<br>

### Oracle 접속하기

-   서버는 항상 IP 또는 호스트 이름을 통해서 접속해야함
    -   내 PC에 설치한 경우 IP / 호스트 이름 : 127.0.0.1 / localhost
    -   회사에서는 별도의 PC에 설치 후 아이디를 공유해서 사용 : IP 주소는 다름

<br>

-   서버에 접속 시 필요한 정보
    -   IP 또는 호스트 이름 + 포트번호 + 계정 + 비밀번호 + 서비스ID
    -   ex) 127.0.0.1 or localhost + 1521 + system + password + xe(or orcl)

<br>

-   계정은 최초에는 system 절대 관리자 계정을 사용, 사용자 계정 생성 시부터는 사용자 계정으로 접근하면 됨
-   서비스ID는 오라클 다운 시 익스프레스 버전은 xe를 사용하며, 상용 버전을 다운 받은 경우에는 orcl를 사용

<br>

-   오라클 버전 18 이상인 버전은 설치 후 최초 1회 아래 코드 실행해야함
    -   오라클 전체 설정을 변경. 1회 실행 후에는 실행 안해도 됨
    -   `Alter Session set "_ORACLE_SCRIPT" = TRUE;`