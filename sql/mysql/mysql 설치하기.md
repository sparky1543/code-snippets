### MySQL 설치하기

- 설치 파일 다운로드
  - https://dev.mysql.com/downloads/windows/installer/8.0.html
 
1. 둘 중 아래에 있는 MSI Installer 다운로드
2. MySQL Community Downloads 화면에서는 [No thanks, just start my download.] 클릭
![image](https://github.com/user-attachments/assets/a8b06d7c-4f1b-46ba-bca8-3a861421c35e)
3. 설치 시작하고 사용자 계정 컨트롤 창이 나타나면 [예] 클릭
4. [Choosing a Setup Type] > [Custom] 선택
5. [Select Products and Features]
   - [MySQL Servers] – [MySQL Server] – [MySQL Server 8.0] – [MySQL Server 8.0.21 – X64]
   - [Applications] – [MySQL Workbench] – [MySQL Workbench 8.0] – [MySQL Workbench 8.0.21 – X64]
   - [Documentation] – [Samples and Examples] – [Samples and Examples 8.0] – [Samples and Examples 8.0.21 – X86]
   - 위에 3개 각각 선택하고 → 버튼
6. [Installation] 에서 3개 항목 확인 > [Execute] > [Progress]에서 설치 진행 과정 확인
7. 설치가 성공적으로 완료되면 각 항목 앞에 초록색 체크가 표시되고 [Status]가 'Complete'로 변경 > [Next]
8. [High Availability] > 기본값인 'Standalone MySQL Server / Classic MySQL Replication' 선택 > [Next]
9. [Type and Networking] > [Config Type] > 'Development Computer' 선택 > [TCP/IP] 체크된 상태에서 [Port] 번호 '3306' 확인 > [Open Windows Firewall ports for networkaccess] 체크 > [Next]
10. [Authentication Method] > 'Use Legacy Authentication Method' 선택 > [Next]
11. [Accounts and Roles] > 관리자(Root) 비밀번호 설정 > [Next]
12. [Windows Service] > [Windows Service Name] 'MySQL'로 변경 > [Next]
13. [Apply Configuration] > [Execute] 클릭 > 모두 초록색 체크 표시되면 > [Finish]
14. [Connect To Server] > 비밀번호 입력 > [Check] > 'Connection succeeded'로 변경되면 > [Next]
15. [Installation Complete] > [Start MySQL Workbench after Setup] 체크 해제 > [Finish]

16. 설치 완료

<br>

### MySQL과 Jupyter Notebook 연동하기

1. Jupyter Notebook 라이브러리 설치 `pip install PyMYSQL`

```
import pymysql
```

2. Connection 하기

```
conn = pymysql.connect(host='localhost'
                       ,user = 'root'
                       ,password = 'password'
                       ,db='testdb'
                       ,charset='utf8'
                       ,cursorclass=pymysql.cursors.DictCursor) # 컬럼명까지 조회하는 속성
cursor = conn.cursor()

# SQL문 작성하기
sql = "SELECT * FROM train"
# SQL문 실행하기
cursor.execute(sql)
# 조회결과 가져오기
result = cursor.fetchall

# 실행 결과 출력
for data in result:
    print(data)

# 커밋 해제
conn.commit() # 커밋은 반복할 필요 없음
conn.close()
```

3. 출력값 DataFrame으로 만들기

```
pd.DataFrame(result)
```
