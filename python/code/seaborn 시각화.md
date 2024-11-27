# seaborn 시각화

`import seaborn as sns` : 고급 시각화 라이브러리, 데이터셋 제공

### 데이터셋 불러오기

-   `sns.load_dataset()` : seaborn에서 제공하는 데이터셋 불러오기
    -   iris, titanic, tips, flights 등

<br>

### 그래프 그리기

-   `sns.set_palette()` : 그래프 색상 변경하기
    -   기본 팔레트 색상 : deep, muted, pastel, bright, dark, colorblind
-   `sns.lineplot(x, y, data)` : 선 그래프 그리기
    -   hue : 변량에 따라 색을 다르게 표시

-   `sns.barplot(x, y, data)` : 막대 그래프 그리기
    -   오차 막대 : 비교 데이터간의 차이를 표시함 
    -   errorbar=None : 오차 막대를 표시하지 않음

-   `sns.stripplot(x, y, data)` : 산점도 그래프 그리기
-   `sns.boxplot(x, y, data)` : 박스플롯 그래프 그리기
    -   orient : h - 가로, v - 세로

-   `sns.distplot(data)` : 히스토그램 그래프 그리기
-   `sns.kdeplot(data)` : 커널 밀도 그래프 그리기
-   `sns.countplot(x, data)` : 빈도 그래프 그리기
-   `sns.jointplot(x, y, data, kind)` : 조합 그래프 그리기
    -   kind="scatter" : 커널 밀도와 산점도 그래프
    -   kind="kde" : 등고선 그래프

-   `sns.violinplot(x, y, data)` : 바이올린플롯 그래프 그리기
-   `sns.pairplot(data)` : 다변량 시각화 그래프 그리기

<br>

### 히트맵 그리기

-   x, y, z 값 3개가 필요함
-   색상이 흐릴수록 값이 적고, 색상이 진할수록 값이 많은 것
-   히트맵에 넣는 데이터의 형태는 피벗테이블 형태
-   이상 패턴이 보이는 시점을 확인 할 수 있음

-   `sns.heatmap(data)` : 히트맵 그래프 그리기
    -   annot : value 값 표현하기(True), 숨기기(False)
    -   fmt=".0f" : float 타입으로 소수점 자릿수 정하기
    -   cmap : color map 지정하기

```
# 그래프 크기 지정
plt.figure(figsize=(16, 10))

# 히트맵 그리기
sns.heatmap(df_pivot, annot=True, fmt=".0f", cmap="rocket_r")

# 그래프 제목 지정
plt.title("년도 및 월별 중국 관광객 추이")

plt.show()
```
