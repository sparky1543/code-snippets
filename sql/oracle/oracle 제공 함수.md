# Oracle 제공 함수

### 임시 테이블

-   `Dual` : 함수 및 문자열 처리에 대한 테스트용 테이블. 1행 1열만 들어있음

```
Select *
From dual;
```

<br>

### 문자 통합 함수

-   `||` : 왼쪽과 오른쪽을 합쳐줌
-   `Concat()` : 왼쪽 오른쪽 합쳐줌. 두 개까지만 가능하며 함수 안에 함수 넣어서 사용

```
/* 주소 1과 주소 2 합치기 */
Select (mem_add1 || ' ' || mem_add2) as mem_add,
        Concat(Concat(mem_add1, ' '), mem_add2) as mem_add2  
From member;
```

<br>

### 아스키 코드 함수

-   `Chr()` : 아스키코드 숫자를 문자로 변환
-   `Ascii()` : 문자를 아스키코드 숫자로 변환

```
/* 문자 A의 아스키 코드 65 */
Select Chr(65), Ascii('A'),
From dual;
```

<br>

### 대소문자 변경 함수

-   `Upper()` : 대문자로 모두 바꾸기
-   `Lower()` : 소문자로 모두 바꾸기
-   `InitCap()` : 단어 중 첫글자만 대문자로 바꾸기

```
/* 대소문자 변경하기 */
Select Upper('hello'), Lower('HeLLo'), InitCap('abcd efg hij')
From dual;
```

<br>

### 공간 채우기 함수

-   `Lpad()` : 전체 n자리 공간을 만들고 오른쪽부터 값을 채운 후 빈 공간은 지정한 문자로 채우기
-   `Rpad()` : 전체 n자리 공간을 만들고 왼쪽부터 값을 채운 후 빈 공간은 지정한 문자로 채우기
    -   값이 한글이 아닌 경우, 공간은 1개씩 차지함
    -   값이 한글인 경우, 공간은 2개씩 차지함
    -   타입 설정할 때는 한글이 3자리지만, 함수에 사용할 때는 한글은 2자리

```
/* 빈 공간 채우기 */
Select Lpad(mem_id, 6, '*') as lpad_mem_id,
       Rpad(mem_id, 6, '*') as rpad_mem_id
From member;
```

<br>

### 공백 제거 함수

-   `LTrim()` : 왼쪽 공백 제거하기
-   `RTrim()` : 오른쪽 공백 제거하기
-   `Trim()` : 양쪽 공백 제거하기

```
/* 공백 제거 확인하기 */
Select '-' || LTrim('    abcd     ') || '-' as ltrim,
       '-' || RTrim('    a b c    d     ') || '-' as rtrim,
       '-' || Trim('   test aaa     ') || '-' as trim
From dual;
```

<br>

### 문자열 자르기 함수

-   `Substr()` : 문자열을 원하는 곳에서 잘라서 가져오기

```
/* 문자열 자르기 */
Select Substr('abcdefg', 0, 2) as s1, -- sql에서는 1부터 시작이라 0이라고 해도 1부터 시작함
       Substr('abcdefg', 1, 2) as s2,
       Substr('abcdefg', -1) as s3, -- 맨 뒤에서 첫번째 값 가져오기
       Substr('abcdefg', -3) as s4 -- -3번째 위치부터 뒷부분 전체 가져오기
From dual;
```

<br>

### 데이터 치환 함수

-   `Replace()` : 데이터의 일부분을 찾아서 다른 데이터로 치환하기

```
/* 데이터 치환하기 */
Select Replace('안녕하세요 파이썬! 공부하세요', '하세요', '반가워')
From dual;

>> 결과 : 안녕반가워 파이썬! 공부반가워
```

<br>

### 문자열 길이 확인 함수

-   `Length()` : 문자의 순수 갯수 확인하기
-   `LengthB()` : 문자의 바이트 갯수 확인하기

```
/* 문자열 길이 확인하기 */
Select Length('abcd한글'), LengthB('abcd한글')
From dual;

>> 결과 : 6, 10
```

<br>

### 절댓값과 제곱 함수

-   `ABS()` : 숫자의 절댓값 조회하기
-   `Power()` : 숫자의 제곱승 조회하기

```
/* 절댓값 조회하기 */
Select ABS(-365), ABS(365), ABS(null)
From Dual;

>> 결과 : 365, 365, (null)

/* 제곱승 조회하기 */
Select power(2,2), power(2,3)
From dual;

>> 결과 : 4, 8
```

<br>

### 가장 큰 값과 작은 값 추출 함수

-   `Greatest()` : 가장 큰 값 추출하기
-   `Least()` : 가장 작은 값 추출하기

```
/* 가장 큰 값과 가장 작은 값 추출*/
-- 문자열은 아스키 코드 값으로 비교
Select Greatest(10, 50, 20, 40), Greatest('A', 'a', 'b'),
        Least(10, 50, 20, 40), Least('A', 'a', 'b')   
From dual;
```

<br>

### 반올림과 절삭 함수

-   `Round()` : 숫자를 반올림해주는 함수
-   `Trunc()` : 숫자를 절삭(버림)해주는 함수

```
/* 반올림과 절삭 함수 */
Select Round(1234.567, -2) as r1,
       Round(1234.567, -1) as r2,
       Round(1234.567, 0) as r3,
       Round(1234.567, 1) as r4,
       Round(1234.567, 2) as r5,
       Trunc(1234.567, 2) as t
From dual;
```

<br>

### 나머지 값 구하는 함수

-   `mod()` : 나눈 나머지의 값 추출하기

```
/* 나머지 값 구하기 */
Select Mod(10, 2), Mod(10, 3)
From dual;
```