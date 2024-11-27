# Open API 데이터 수집

### 사용하는 라이브러리

-   `import pandas as pd` : 데이터프레임 다루기 위한 라이브러리
-   `from bs4 import BeautifulSoup` : 웹 문서 처리 라이브러리
-   `import requests` : 웹에서 요청/응답을 처리하는 라이브러리

<br>

### 시작 전 설치할 것

-   `pip install lxml` : lxml 포맷을 사용하기 위한 패키지 설치

<br>

### Open API 데이터 불러오기

-   서비스 인증키(encoding key) : 데이터 요청 시 사용  
    -   응답하는 서버에서 인증키가 없으면 응답 안함
    -   apikey 변수에 인증키 담아서 사용

-   numOfRows, pageNo 등 : 요청시 사용하는 파라미터
-   요청 url : 요청 url에 요청 파라미터 변수들을 넣어서 보내야 함

```
# 서비스 인증키(encoding key)
apikey="--서비스 인증키 받아서 넣기--"

# 요청시 사용하는 파라미터
numOfRows = 10
pageNo = 1

# 요청 URL
url = "--서비스 URL--?schAirportCode=GMP&serviceKey={key}&numOfRows={nrow}&pageNo={pno}"

# 요청 URL에 파라미터 값 넣기
api_url = url.format(key = apikey, 
                     nrow = numOfRows, 
                     pno = pageNo)
```

-   URL을 이용해서 서버에 요청하기
    -   `requests` : 웹에서 URL을 이용해서 전송시 사용하는 라이브러리
    -   `get()` : 요청에 따른 응답 결과를 받아오는 함수

-   텍스트로 변환하여 받아오기  
    -   `text` : 응답 결과를 텍스트로 변환

-   xml 문서 포맷 정의하기 (parser)  
    -   `BeautifulSoup(data, "포맷")` : 문자열을 문서 포맷(xml, html)으로 변환

-   태그 이름을 이용해서 태그 값 추출하기
    -   리스트 형태로 반환해줌
    -   `find_all()` : 태그 이름이 있는 모든 태그 조회
    -   `find()` : 태그 이름이 있는 한개 태그만 조회

-   태그 사이에 들어있는 값 추출하기
    -   `text` : 태그 사이의 값을 문자열 타입으로 가져옴

```
# url을 이용해서 요청하기
rs_data = requests.get(api_url)

# 1. 텍스트로 변환하여 받아오기
rs_text = rs_data.text

# 2. xml 문서 포맷 정의하기
rs_xml = BeautifulSoup(rs_text, "lxml")

# 3. 원하는 값이 들어있는 태그 이름을 이용해서 태그 추출하기
rs_xml.find_all("airportkor")

# 4. 태그 사이에 들어있는 값 추출하기
# 웹에서 가져온 데이터는 모두 문자열 타입
rs_xml.find_all("airportkor")[0].text
```

<br>

### 데이터프레임으로 변환하기

```
# 컬럼명만 있는 빈 데이터프레임 생성
df = pd.DataFrame(columns=["공항명"])

# Open API 데이터 불러오기
api_url = url.format(key = apikey, 
                       nrow = numOfRows, 
                       pno = pageNo)
rs_data = requests.get(api_url)
rs_text = rs_data.text
rs_xml = BeautifulSoup(rs_text, "lxml")

# for문으로 데이터 불러와서 행단위로 추가하기
for i in range(len(rs_xml.find_all("airportkor"))):
    list_nm = [rs_xml.find_all("airportkor")[i].text]
    df.loc[len(df)] = list_nm
```
