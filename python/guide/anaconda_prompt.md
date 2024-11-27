# Anaconda Prompt 사용법

### 버전 확인하기

-   파이썬 버전 확인 : `python —version`
-   아나콘다 버전 확인 : `conda —version`

<br>

### 가상환경

-   가상환경 설치 위치 : base 가상환경 위치에서 진행
-   디렉토리 위치 : 어디든 무관. 아나콘다가 알아서 생성

-   가상환경 생성하기 : `conda create -n 가상환경이름 python=버전`
-   가상환경 삭제하기 : `conda env remove -n 삭제할 가상환경이름`
-   가상환경 활성화시키기 : `conda activate 가상환경이름`
-   가상환경 비활성화시키기 : `conda deactivate`
-   가상환경 목록 확인하기 : `conda env list`

-   설치 명령어 (⚠️ 생성한 가상환경에서 진행하기)
    -   conda : 아나콘다 라이브러리 이용하여 설치. 최적화된 버전으로 설치됨
    -   pip : 외부 라이브러리 이용하여 설치. 인터넷 연결 필요. 최신 버전으로 설치됨
-   라이브러리 설치 명령어
    -   `conda install -c conda-forge 모듈명==버전` 또는 `conda install 모듈명==버전`
    -   `pip install 모듈명==버전`
-   가상환경에 설치된 라이브러리 목록 확인
    -   `conda list` : conda 명령으로 설치된 목록 확인
    -   `pip list` : pip 명령으로 설치된 목록 확인
-   주피터 노트북 설치하기 : `pip install jupyter notebook`

<br>

### 커널

-   커널 생성하기
    -   `python -m ipykernel install --user --name 가상환경이름 --display-name 커널이름`
    -   프로그램 tool에서 가상환경 라이브러리 이용하기 위해 커널 생성
    -   커널은 가상환경 1개당 1개만 만들어서 사용함
    -   커널 생성 전에 주피터 노트북이 설치되어 있어야함
-   커널 목록 확인하기 : `jupyter kernelspec list`
-   커널 삭제하기
    -   `jupyter kernelspec uninstall 가상환경이름`
    -   커널 삭제할 때 이름은 커널 목록에 보이는 이름(가상환경이름)으로 사용

<br>

### 라이브러리

-   가상환경 생성 시 기본적으로 설치해놓는 라이브러리
    -   `pip install ipython jupyter matplotlib pandas xlrd seaborn scikit-learn`
    -   `pip install openpyxl` : 엑셀 파일 처리

> ⚠️ scikit-learn : 머신러닝 라이브러리 (python 3.9 이하 버전용)  
> ⇒ 향후 오류 발생 시 pip install sklearn 설치 (python 3.10 이상 버전용)

<br>

### 실행하기

-   Anaconda Prompt 열기
-   작업디렉토리 위치로 이동하기
    -   `dir/w` 디렉토리 확인
    -   `cd /` 루트로 넘어가기
    -   `cd 폴더경로` 폴더로 이동
-   가상환경 활성화시키기 conda activate 가상환경이름
-   에디터 열기 jupyter notebook
-   에디터 중지하기 \[Ctrl\] + c

<br>

### 참고사항

-   화면 클리어 : cls
-   복사하기 : 드래그 후 마우스 우클릭
-   선택 Anaconda prompt : 코드 작성이나 실행이 안됨. 마우스 우클릭해서 해제
-   prompt 창을 끄면 자동으로 연결이 끊어짐