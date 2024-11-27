# folium 지도 시각화

`import folium` : 지도 시각화에 사용하는 라이브러리

`conda install -c conda-forge folium` : 처음 folium 사용하기 전 설치하기

<br>

### 기본 지도 그리기

-   `folium.Map()` : 지도를 그리는 클래스
    -   location : 최초에 보여줄 지도의 중심 위치 지정. 위/경도를 이용해 지정함
        -   \[37.573050, 126.979189\] : 서울 중심점
    -   tiles : 지도 스타일 지정하기
        -   "openstreetmap” : 도시형 건물 스타일
        -   "Stamen Terrain" : 산림 위주의 스타일
        -   "cartoDBpositron" : 하천이나 도로 위주 스타일
        -   "cartoDB dark\_matter" : 하천이나 도로 위주 어두운 스타일
    -   zoom\_start : 최초에 보여줄 zoom 사이즈 지정하기

```
map = folium.Map(
                # 서울 중심점
                location = [37.573050, 126.979189],
                # 지도 스타일
                tiles = "openstreetmap",
                # zoom 사이즈 지정
                zoom_start = 50)
map
```
![image](https://github.com/user-attachments/assets/b6cc1401-5f53-4a41-bf32-b6cfad1d3a5a)

<br>

### 마커 표시하기

-   `folium.CircleMarker().add_to()` : 지도에 원으로 마킹해주는 클래스
    -   location : 마커의 위치 위/경도로 지정
    -   fill\_color : 마커 내부 색상
    -   fill\_opacity : 마커 불투명도(0~1)
    -   color : 마커 테두리 색상
    -   weight : 마커 테두리 두께
    -   radius : 마커 크기
    -   popup : 팝업 띄우기
    -   tooltip : 마우스 가져다대면 문구 띄우기

```
for idx in df.index :
    lat = df.loc[idx,"위도"]
    lng = df.loc[idx,"경도"]
    
    folium.CircleMarker(
        # 마커의 위치 지정 : 위도, 경도
        location = [lat, lng],
        # 마커 채우기 색상
        fill_color = "green",
        # 마커 불투명도
        fill_opacity = 0.3,
        # 마커 테두리 색상
        color = "darkgreen",
        # 마커 테두리 두께
        weight = 1,
        # 마커 크기
        radius = 5
    ).add_to(map)
```

![image](https://github.com/user-attachments/assets/e9f1b00d-cb34-4b46-bb38-65ddf43f5988)

-   `folium.Marker().add_to()` : 지도에 기본 마커로 마킹해주는 클래스
    -   icon=folium.Icon() : 마커모양 지정
        -   color : 마커 색상 지정
        -   icon : 마커 안의 아이콘 지정

-   popup으로 이미지 띄우기 : html 코드로 불러오기
    -   ```<img src="" width="" height="">``` : 이미지 주소/위치, 가로, 세로 지정
    -   ```<br /><span>내용</span>``` : 텍스트 지정

```
for idx in df.index :
    lat = df.loc[idx,"위도"]
    lng = df.loc[idx,"경도"]
    img = df.loc[idx,"이미지"]
    place = df.loc[idx,"장소명"]
    gugun = df.loc[idx,"구군"]
    
    htmlcode = """<div>
    <img src="{}" width="300" height="200">
    <br /><span> </span>
    <br /><span>장소명 : {}</span>
    <br /><span>구군 : {}</span>
    </div>""".format(img, place, gugun)
    tooltip = "Click!"
    
    folium.Marker(
        location = [lat, lng],
        icon=folium.Icon(color='orange',icon='star'),
        popup=htmlcode,
        tooltip=tooltip
    ).add_to(map)
```

![image](https://github.com/user-attachments/assets/769841f4-a94d-40a7-a99f-d6f3efde15dc)

<br>

### 경계면 표시하기

-   `folium.GeoJson().add_to()` : 경계면 그려주는 클래스
    -   geojson 변수 : 경계면 데이터
    -   style\_function : 스타일 지정하기. 딕셔너리 형태로 지정
        -   opacity : 불투명도
        -   weight : 두께
        -   color : 색상

```
folium.GeoJson(
    # 경계면 데이터
    seoul_sgg,
    # 스타일  넣기
    style_function = {"opacity" : 0.5, "weight" : 0.6, "color" : "yellow"}
).add_to(map)
```

![image](https://github.com/user-attachments/assets/10c32c3c-96f0-49e7-a3a0-0ac916b9ab73)

-   `folium.Choropleth().add_to()` : 경계면 그려주는 클래스. 양적 데이터 별로 색상을 다르게 표시
    -   geo\_data : 지도 경계면 데이터
    -   data : 데이터프레임 데이터
    -   columns : 양적으로 사용할 컬럼 지정
    -   fill\_color : 색상맵 지정. 단일 색상 불가
    -   fill\_opacity : 불투명도
    -   line\_opacity : 선 불투명도
    -   key\_on : 데이터프레임의 컬럼명과 경계면 데이터의 매핑할 값 지정

```
folium.Choropleth(
    # 경계면 데이터
    geo_data=seoul_sgg,
    # 데이터프레임 데이터
    data = seoul_sgg_stat,
    # 양적 컬럼 지정
    columns = ["시군구명", "주민등록인구"],
    # 색상맵
    fill_color = "YlGn",
    # 불투명도
    fill_opacity = 0.5,
    # 선 불투명도
    line_opacity = 0.7,
    # 매핑할 값 지정
    key_on = "properties.SIG_KOR_NM" 
).add_to(map)
```

![image](https://github.com/user-attachments/assets/67ee80c5-6248-4b95-9fb9-91dec45ca800)
