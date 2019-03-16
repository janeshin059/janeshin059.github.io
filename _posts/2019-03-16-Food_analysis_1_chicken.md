
## Food analysis in Seoul_ using SK data hub


SK data hub는 SK Telecom에서 제공하는 여러 데이터가 모여있는 곳입니다.
여기서 '1월 서울시 치킨 판매업종 이용 통화량'을 분석해 보았습니다. 
주의해야 할 점은 SK 텔레콤의 통화량 데이터와 업종 데이터를 기반으로 추출한 데이터이기에
전체 치킨집 서비스 이용 현황이 반영되어 있지 않음을 감안하여 데이터를 이용해야 한다는 점입니다.
그러나 모집단에 대한 일종의 표본집단으로 생각해 본다면 이 역시 유의미한 값들을 도출 가능하리라 봅니다.

//

같이 데이터 분석 스터디를 진행하시는 분의 블로그에서 아이디어를 얻었습니다.
원글은 R이며 저는 python으로 진행할 것입니다.
블로그의 주소는 다음과 같습니다.

https://unfinished-god.com/2019/02/25/%EC%84%9C%EC%9A%B8%EC%8B%9C-%EB%A8%B9%EA%B1%B0%EB%A6%AC-%EB%B6%84%EC%84%9D-1%EC%9B%94-%EC%B9%98%ED%82%A8-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EB%B6%84%EC%84%9D/


데이터는 다음의 주소에서 다운받으실 수 있습니다.

https://www.bigdatahub.co.kr/product/view.do?pid=1002028



### STEP 1. Data Preprocessing(데이터 전처리)


```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
```


```python
df = pd.read_csv("C:/Users/user/Desktop/janeshin/skdata/CALL_CHICKEN_01MONTH.csv")
df.head(10)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>기준일</th>
      <th>요일</th>
      <th>성별</th>
      <th>연령대</th>
      <th>시도</th>
      <th>시군구</th>
      <th>읍면동</th>
      <th>업종</th>
      <th>통화건수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190101</td>
      <td>화</td>
      <td>여</td>
      <td>20대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>도곡동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190101</td>
      <td>화</td>
      <td>남</td>
      <td>30대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>삼성동</td>
      <td>치킨</td>
      <td>36</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190101</td>
      <td>화</td>
      <td>여</td>
      <td>10대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>대치동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190101</td>
      <td>화</td>
      <td>여</td>
      <td>40대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>대치동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190101</td>
      <td>화</td>
      <td>여</td>
      <td>40대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>일원동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>20190101</td>
      <td>화</td>
      <td>남</td>
      <td>10대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>논현동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>20190101</td>
      <td>화</td>
      <td>여</td>
      <td>30대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>일원동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>20190101</td>
      <td>화</td>
      <td>남</td>
      <td>50대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>대치동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>20190101</td>
      <td>화</td>
      <td>남</td>
      <td>30대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>수서동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>20190101</td>
      <td>화</td>
      <td>남</td>
      <td>20대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>논현동</td>
      <td>치킨</td>
      <td>18</td>
    </tr>
  </tbody>
</table>
</div>




```python
df['기준일'].unique()
```




    array([20190101, 20190102, 20190103, 20190104, 20190105, 20190106,
           20190107, 20190108, 20190109, 20190110, 20190111, 20190112,
           20190113, 20190114, 20190115, 20190116, 20190117, 20190118,
           20190119, 20190120, 20190121, 20190122, 20190123, 20190124,
           20190125, 20190126, 20190127, 20190128, 20190129, 20190130,
           20190131], dtype=int64)



모든 날짜에 대해 데이터가 존재한다는 점을 확인할 수 있습니다.


##### 빈 값이 있는지 체크해봅시다.

dataframe에 있어서 빈 값이 있는지의 체크는 다음과 같은 방법으로 할 수 있습니다.

1. (모든 데이터에 대해 null여부 체크 원하는 경우)df.isnull을 통해 null값인지에 대한 boolean value를 받는 경우

df.isnull()

2. (null인 값의 개수를 원하는 경우)

df.isnull.sum()
:각 column에 대한 null개수

아래의 링크를 참조하면 됩니다.

https://chartio.com/resources/tutorials/how-to-check-if-any-value-is-nan-in-a-pandas-dataframe/



```python
df.isnull().sum()
```




    기준일     0
    요일      0
    성별      0
    연령대     0
    시도      0
    시군구     0
    읍면동     0
    업종      0
    통화건수    0
    dtype: int64




```python
df.isnull().sum().sum()
```




    0



각 행들을 살펴봅시다.


```python
df['기준일'].value_counts()
```




    20190125    1147
    20190112    1060
    20190111    1056
    20190118    1049
    20190126    1046
    20190105    1022
    20190116    1018
    20190122    1015
    20190119    1014
    20190104    1003
    20190127     995
    20190120     975
    20190113     974
    20190101     965
    20190106     952
    20190115     944
    20190108     939
    20190123     938
    20190124     938
    20190103     935
    20190110     935
    20190131     929
    20190109     923
    20190117     918
    20190130     907
    20190107     890
    20190121     885
    20190102     884
    20190129     876
    20190128     860
    20190114     858
    Name: 기준일, dtype: int64



2019년 1월 25일에 무슨 일이 있었길래 이렇게 치킨이 많이 팔렸지?하고 검색해보니
아시안컵 8강 이었군요. (ㅠㅠ)
1월 12일도 마찬가지로 키르기스스탄과의 경기였고요.
축구 +주말(금,토,일) 외의 여러 요소들이 영향을 끼쳤다고 보입니다.


```python
df['시군구'].value_counts()
```




    강남구     2381
    강서구     1916
    중구      1717
    영등포구    1688
    마포구     1552
    서대문구    1476
    서초구     1415
    구로구     1396
    성북구     1377
    용산구     1352
    강동구     1295
    송파구     1162
    동작구     1135
    동대문구    1084
    은평구     1013
    노원구      993
    중랑구      914
    종로구      906
    강북구      868
    성동구      860
    양천구      839
    금천구      831
    광진구      678
    관악구      560
    도봉구      442
    Name: 시군구, dtype: int64



신기한 점은, 이 결과가 서울시 인구 순위와는 비례하지 않는다는 것입니다.
중구의 경우 서울시 전체에서 인구가 가장 적은데 저 순위에는 높군요.
중구는 낮에 유입된 인구와 밤에 빠져나가는 인구(퇴근 등) 의 차이가 큰데

서울시 인구 순위는 실제 거주민만을 대상으로 하고 있어서 그런지 치킨 주문 수와는 비례하지 않습니다.
중구에  실제 거주하는 사람들만이 치킨을 시켜 먹는건 아닐 테니까요.

### STEP 2. 어떻게 분석을 해볼까?Domain Knowledge


데이터에 대해 어느 정도 살펴보았으니
이제는 어떠한 식으로 이 data를 다룰지 생각해 봅시다.

요식업계에 대한 지식은 거의 없지만 몇 가지 가설을 생각해 봅시다.


1. 연령대에 따라 다르지 않을까?

   - 치킨은 아무래도 10~30대에게 더 친숙한 음식이고,이 중에서 10대보다는 20,30대가 경제력이 있다고 판단되므로 20~30대가 40대 이상보다 주문을 많이 하지 않을까?
   
2. 요일에 따라 주문 건수가 달라질까?

   - 금/토에 많이 주문을 하지 않을까?

3. 스포츠 경기나 중요한 행사 등과 상관이 있지 않을까?

   -  스포츠 경기가 있는 날에 주문을 많이 할 듯하다




### groupby()로 그룹별 집계하기

파이썬의 groupby() 연산자를 사용하여 집단 및 그룹별로 데이터를 집계,
요약해 보겠습니다.

전체 데이터를 그룹 별로 split하고
-> 각 그룹별로 집계함수를 apply한후
-> 그룹별 집계 결과를 하나로 합치는 combine단계를 거치게 됩니다.
(split->apply function ->combine)



더 자세한 내용은
https://rfriend.tistory.com/383
를 참조하시기 바랍니다.




```python
df['통화건수'].describe() #descriptive statics
```




    count    29850.000000
    mean        13.243987
    std         17.464655
    min          5.000000
    25%          5.000000
    50%          5.000000
    75%         14.000000
    max        242.000000
    Name: 통화건수, dtype: float64



이제는 '연령대' 그룹 별로 '통화건수' 변수에 대해 groupby집계를 해 보겠습니다.
(연령대별로 얼마나 통화를 많이 했는지 알고 싶으므로)
집단별 크기는 grouped.size()
집단별 합계는 grouped.sum()
집단별 평균은 grouped.mean()을 사용합니다


```python
groupedByAge = df['통화건수'].groupby(df['연령대'])

groupedByAge.sum()
```




    연령대
    10대       26681
    20대       65140
    30대       95924
    40대      122028
    50대       56655
    60대이상     28905
    Name: 통화건수, dtype: int64




```python
groupedByAge.mean()
```




    연령대
    10대       7.234544
    20대      11.438104
    30대      15.684107
    40대      20.057199
    50대      12.487326
    60대이상     7.749330
    Name: 통화건수, dtype: float64



검증해 본 결과 가설과는 다르게, 40대가 가장 많은 구매를 한 것으로 드러났습니다.


이제는 요일에 따른 주문 건수를 살펴보도록 하겠습니다.



```python
groupedByDay = df['통화건수'].groupby(df['요일'])


groupedByDay.sum().sort_values(ascending = False) # sort_values를 사용해 내림차순으로 정리
```




    요일
    토    64817
    금    63117
    화    59152
    일    58460
    목    55768
    수    55211
    월    38808
    Name: 통화건수, dtype: int64



토요일과 금요일의 주문량이 다른 날들에 비해 많다는 것을 알 수 있습니다.
마지막으로, 앞에서 살펴본 것에 따르면 스포츠 경기의 전날에 치킨 주문량이 많았던 경우가 있습니다.
이제는 이를 바탕으로 스포츠 경기의 스케줄과 치킨 주문량 사이의 관계에 대해서 살펴 보겠습니다.

2019 아시안컵 대한민국 일정은 다음과 같습니다.
- 1차전(대한민국:필리핀)-> 190107 오후 10:30
- 2차전(대한민국:키르기스스탄)->190112 오전 1시
- 3차전(대한민국:중국)->190116 오후 10:30
- 16강(대한민국:바레인)->190122 오후 10시
- 8강(대한민국:카타르)->190125 오후 10시

이제 이 데이터들을 갖고 dataframe을 만들어보겠습니다.




```python
soccer = {'Date':['20190107','20190112','20190116','20190122','20190125'],
         'Country':['Korea:Philippines','Korea:Kyrgyzstan','Korea:China','Korea:Bahrain','Korea:Qatar']
         ,'Name':['1','2','3','16','8']}

soccer_frame =pd.DataFrame(soccer)

soccer_frame.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Date</th>
      <th>Country</th>
      <th>Name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>20190107</td>
      <td>Korea:Philippines</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>20190112</td>
      <td>Korea:Kyrgyzstan</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>20190116</td>
      <td>Korea:China</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>20190122</td>
      <td>Korea:Bahrain</td>
      <td>16</td>
    </tr>
    <tr>
      <th>4</th>
      <td>20190125</td>
      <td>Korea:Qatar</td>
      <td>8</td>
    </tr>
  </tbody>
</table>
</div>



이제 해당 Date에 대한 치킨 주문량을 살펴보도록 하겠습니다.
두 개의 다른 dataframe을 사용합니다.


```python
groupedBysoccer = df['통화건수'].groupby(soccer_frame['Date'])
groupedBysoccer.sum() #error
```




    Date
    20190107     5
    20190112    36
    20190116     5
    20190122     5
    20190125     5
    Name: 통화건수, dtype: int64



음?뭔가 이상합니다. 이렇게 적게 나올 리가 없는데..

1. soccer_frame의 date와 동일한
2. df에 있는 Date를 찾아서
3. 그걸로 묶는다

이러한 방식으로, 새로운 dataframe을 만들도록 하겠습니다.
여기서는 rows들을 multiple values present in an iterable or list들을 참조해 필터링 할 것입니다.

여기서는 soccer_frame의 date와 동일한 df에 있는 date를 찾고 싶은 것입니다.
이는 soccer_frame의 date와 동일한 row만을 필터링 할 수 있다는 의미입니다.

자세한 자료는 다음을 참조하시면 됩니다.
https://cmdlinetips.com/2018/02/how-to-subset-pandas-dataframe-based-on-values-of-a-column/


```python
years = soccer_frame['Date']

df['기준일'].isin(years)

soccerY = df[df['기준일'].isin(years)]

soccerY.head()



```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>기준일</th>
      <th>요일</th>
      <th>성별</th>
      <th>연령대</th>
      <th>시도</th>
      <th>시군구</th>
      <th>읍면동</th>
      <th>업종</th>
      <th>통화건수</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5761</th>
      <td>20190107</td>
      <td>월</td>
      <td>남</td>
      <td>30대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>삼성동</td>
      <td>치킨</td>
      <td>23</td>
    </tr>
    <tr>
      <th>5762</th>
      <td>20190107</td>
      <td>월</td>
      <td>여</td>
      <td>60대이상</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>역삼동</td>
      <td>치킨</td>
      <td>6</td>
    </tr>
    <tr>
      <th>5763</th>
      <td>20190107</td>
      <td>월</td>
      <td>여</td>
      <td>50대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>수서동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5764</th>
      <td>20190107</td>
      <td>월</td>
      <td>남</td>
      <td>20대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>대치동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5765</th>
      <td>20190107</td>
      <td>월</td>
      <td>여</td>
      <td>40대</td>
      <td>서울특별시</td>
      <td>강남구</td>
      <td>일원동</td>
      <td>치킨</td>
      <td>5</td>
    </tr>
  </tbody>
</table>
</div>



잘 걸러진 것을 확인할 수 있습니다.


```python
groupedBysoccerY = soccerY['통화건수'].groupby(soccerY['기준일'])
groupedBysoccerY.mean()
# 통화건수 대로 더한거라 앞 값과 차이가 있을 수 있습니다.
```




    기준일
    20190107    11.776404
    20190112    15.460377
    20190116    13.851670
    20190122    13.829557
    20190125    17.166521
    Name: 통화건수, dtype: float64




```python
df['통화건수'].mean()
```




    13.243986599664991



평균보다 높은 Date들이 많다는 것을 알 수 있다.

### 의문점


1. '날짜가 나온 횟수'(ex: 2019년 1월 1일에 해당하는 row가 몇 개인지) or '날짜가 나온 통화건수의 합계'
이 둘 중 어느 것이 치킨 주문량에 대해 더 적합한 결과를 나타낼 수 있을까?
-> 어떤 사람은 통화건수가 66건이나 되던데, 이는 '하루에 했던통화건수'일까 '그 사람이 1월달동안 한 전체 통화건수'일까?(이에 대해서는 sk에 별도의 설명이 되어 있지 않다. data를 올려놓을거면 설명을 충실하게 했으면 좋겠다..


