# Git 시작하기

Git은 프로젝트의 시간과 차원을 자유롭게 넘나들수 있도록 해준다.
- 시간 : 프로젝트의 버전을 과거로 되돌리거나 특정 내역 취소 가능
- 차원 : 프로젝트의 여러 모드를 쉽게 전환하고 관리 가능

<br>

### Git 설치하기

- 설치 파일 다운로드
  - [https://git-scm.com/](https://git-scm.com/)
  - 설치 과정에서 반드시 **Git Bash** 포함하기

- 설치 후 테스트
  - ```git --version``` : 버전 확인하기
  - ```git config --global core.autocrlf true``` : 윈도우와 맥의 엔터 방식 차이로 인한 오류 방지
 
- VS Code의 기본 터미널 설정
  - VS Code 에서 ```Ctrl``` + ```Shift``` + ```P```
  - Select Default Profile 검색하여 선택
  - **Git bash** 선택
  - Git bash를 **C 드라이브**에 설치해야 설정 가능

<br>

### Git 설정하기

터미널 프로그램 (Git Bash, iTerm2)에서 아래 명령어 실행

- Git 전역으로 사용자 이름과 이메일 주소 설정
  - ```git config --global user.name "(본인 이름)"```
  - ```git config --global user.email "(본인 이메일)"```

- 기본 브랜치명 변경
  - ```git config --global init.defaultBranch main```

<br>

### Git 관리 시작하기
원하는 위치에 폴더 생성하고 VS Code로 열기

- 관리 시작하기 : ```git init```
- 변경사항 확인하기 : ```git status```
- 모든 파일 담기 : ```git add .```
- 커밋 메시지와 함께 커밋하기 : ```git commit -m "commit message"```
- 추가와 커밋 한번에 : ```git commit -am "commit message"```
- 결과 확인 및 종료 : ```git log``` ```:q```

<br>

### Github 사용하기
새 레포지토리 생성 후 코드 복사해서 원격 저장소 연결하기

- 커밋 밀어올리기 : ```git push```
- 커밋 당겨오기 : ```git pull```
