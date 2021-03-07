# AT 농산물 시세 open api 활용   
<img src="https://user-images.githubusercontent.com/71205453/110237763-0ec17400-7f81-11eb-92f6-e16a9bdbc23d.png" width = 600>

### 1. 선정이유    
재학시절 농식품 가격분석론이란 과목을 수강하게 되면서 농산물의 과거 월별 시세 데이터가 있으면 가격예측이 가능함을 알게 되었고 그 당시에는 과제로 인삼시세를 가격예측 하였었다.   
![image](https://user-images.githubusercontent.com/71205453/110237849-960ee780-7f81-11eb-927a-70d3cd87582d.png)
따라서 AT에서 제공하는 api를 통해 얻는 데이터를 활용한다면 알고리즘을 적용한 가격예측을 좀 더 편리하게 할 수 있겠다고 판단하였다.   

### 2. 제공 되어지는 AT 농산물시세 api   
https://www.kamis.or.kr/customer/reference/openapi_list.do   
1	일별 부류별 도.소매가격정보   
2	일별 품목별 도·소매가격정보   
3	월별 도.소매가격정보   
4	연도별 도.소매가격정보   
5	친환경농산물 가격정보('05~'20.3.)   
6	최근일자 도.소매가격정보(상품 기준)   
7	최근 가격추이 조회(상품 기준) ※ 6번 API와 연동해서 사용가능 (품목코드 연계)   
8	월평균 가격추이 조회(상품 기준) ※ 6번 API와 연동해서 사용가능 (품목코드 연계)   
9	연평균 가격추이 조회(상품 기준) ※ 6번 API와 연동해서 사용가능 (품목코드 연계)   
10	최근일자 지역별 도.소매가격정보(상품 기준)   
11	친환경농산물 품목별 가격정보('05~'20.3.)   
12	친환경농산물 가격정보('20.4~)   
13	친환경농산물 품목별가격정보('20.4~)   
14	지역별 품목별 도.소매가격정보   

**-예시-**   
**6번 api인	최근일자 도.소매가격정보(상품 기준)으로 확인해본 2010년 10월 1일 배추 시세**   
![image](https://user-images.githubusercontent.com/71205453/110237868-b2ab1f80-7f81-11eb-9a4b-13a93766d07c.png)

### 3. 계절성 가격 예측을 위한 농산물 월별 시세 데이터 만들기   
흔히 가격예측은 추세(trend), 계절성(seasonality), 특정 이벤트(holiday)를 기준으로 예측합니다.   
**월별로 가격을 예측하는 계절성(seasonality) 예측에는 다년간의 월별 평균 시세가 필요하므로 api를 통해 데이터 셋을 만들어 주었습니다.**   
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>m1</th>
      <th>m2</th>
      <th>m3</th>
      <th>m4</th>
      <th>m5</th>
      <th>m6</th>
      <th>m7</th>
      <th>m8</th>
      <th>m9</th>
      <th>m10</th>
      <th>m11</th>
      <th>m12</th>
      <th>avg</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1996</th>
      <td>33850</td>
      <td>33508</td>
      <td>33325</td>
      <td>34158</td>
      <td>35135</td>
      <td>34924</td>
      <td>34154</td>
      <td>34174</td>
      <td>34850</td>
      <td>35229</td>
      <td>34850</td>
      <td>34850</td>
      <td>34429</td>
    </tr>
    <tr>
      <th>1997</th>
      <td>34850</td>
      <td>34929</td>
      <td>35210</td>
      <td>35576</td>
      <td>35800</td>
      <td>35800</td>
      <td>36025</td>
      <td>37180</td>
      <td>36691</td>
      <td>35423</td>
      <td>34896</td>
      <td>34932</td>
      <td>35616</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>35650</td>
      <td>35775</td>
      <td>35800</td>
      <td>35800</td>
      <td>35800</td>
      <td>36081</td>
      <td>36927</td>
      <td>38585</td>
      <td>38785</td>
      <td>38333</td>
      <td>38088</td>
      <td>38750</td>
      <td>37059</td>
    </tr>
    <tr>
      <th>1999</th>
      <td>38500</td>
      <td>38500</td>
      <td>39220</td>
      <td>39400</td>
      <td>39852</td>
      <td>40350</td>
      <td>40500</td>
      <td>40500</td>
      <td>40500</td>
      <td>40496</td>
      <td>40100</td>
      <td>40100</td>
      <td>39865</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>40954</td>
      <td>40524</td>
      <td>40955</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>40500</td>
      <td>40500</td>
      <td>40500</td>
      <td>40854</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>40180</td>
      <td>38125</td>
      <td>38000</td>
      <td>38000</td>
      <td>40052</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38870</td>
      <td>39000</td>
      <td>39231</td>
      <td>41000</td>
      <td>39808</td>
      <td>40000</td>
      <td>40000</td>
      <td>38993</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>40000</td>
      <td>40000</td>
      <td>40000</td>
      <td>40000</td>
      <td>40000</td>
      <td>40250</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>42000</td>
      <td>42000</td>
      <td>40700</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>42000</td>
      <td>42875</td>
      <td>43000</td>
      <td>43000</td>
      <td>42333</td>
      <td>42346</td>
      <td>43000</td>
      <td>43000</td>
      <td>42263</td>
      <td>40667</td>
      <td>38286</td>
      <td>38000</td>
      <td>41891</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>37409</td>
      <td>36000</td>
      <td>35000</td>
      <td>35000</td>
      <td>37264</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>35000</td>
      <td>35000</td>
      <td>34773</td>
      <td>34000</td>
      <td>34350</td>
      <td>35024</td>
      <td>36200</td>
      <td>37545</td>
      <td>38864</td>
      <td>37526</td>
      <td>36095</td>
      <td>36000</td>
      <td>35878</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>36000</td>
      <td>36263</td>
      <td>37000</td>
      <td>37381</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>36545</td>
      <td>36000</td>
      <td>36684</td>
      <td>37142</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>37000</td>
      <td>37833</td>
      <td>39000</td>
      <td>39000</td>
      <td>39000</td>
      <td>39925</td>
      <td>40304</td>
      <td>41000</td>
      <td>41000</td>
      <td>39636</td>
      <td>39000</td>
      <td>39000</td>
      <td>39321</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>39000</td>
      <td>38100</td>
      <td>38000</td>
      <td>38000</td>
      <td>37868</td>
      <td>37500</td>
      <td>36630</td>
      <td>35357</td>
      <td>35000</td>
      <td>33857</td>
      <td>33000</td>
      <td>33000</td>
      <td>36251</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>33000</td>
      <td>33000</td>
      <td>32545</td>
      <td>31795</td>
      <td>30553</td>
      <td>31000</td>
      <td>31000</td>
      <td>30750</td>
      <td>30500</td>
      <td>30500</td>
      <td>33000</td>
      <td>33283</td>
      <td>31762</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>33762</td>
      <td>35324</td>
      <td>36444</td>
      <td>37402</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>40000</td>
      <td>40595</td>
      <td>37666</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>40750</td>
      <td>40000</td>
      <td>40000</td>
      <td>42864</td>
      <td>43000</td>
      <td>41131</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>43000</td>
      <td>43000</td>
      <td>43000</td>
      <td>43000</td>
      <td>43167</td>
      <td>43500</td>
      <td>43500</td>
      <td>43500</td>
      <td>43500</td>
      <td>43452</td>
      <td>42214</td>
      <td>42000</td>
      <td>43065</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>42000</td>
      <td>42000</td>
      <td>42000</td>
      <td>41614</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>41000</td>
      <td>40528</td>
      <td>40000</td>
      <td>40000</td>
      <td>39262</td>
      <td>40953</td>
    </tr>
    <tr>
      <th>2015</th>
      <td>39000</td>
      <td>39000</td>
      <td>38250</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>38000</td>
      <td>35405</td>
      <td>34905</td>
      <td>34500</td>
      <td>37397</td>
    </tr>
    <tr>
      <th>2016</th>
      <td>34000</td>
      <td>34000</td>
      <td>34000</td>
      <td>34000</td>
      <td>34000</td>
      <td>34000</td>
      <td>34000</td>
      <td>33205</td>
      <td>31211</td>
      <td>26550</td>
      <td>30000</td>
      <td>30000</td>
      <td>32409</td>
    </tr>
    <tr>
      <th>2017</th>
      <td>28825</td>
      <td>28000</td>
      <td>28000</td>
      <td>28000</td>
      <td>28000</td>
      <td>28024</td>
      <td>29452</td>
      <td>30432</td>
      <td>32167</td>
      <td>34500</td>
      <td>36841</td>
      <td>38211</td>
      <td>30802</td>
    </tr>
    <tr>
      <th>2018</th>
      <td>38818</td>
      <td>40583</td>
      <td>42019</td>
      <td>42752</td>
      <td>42850</td>
      <td>43063</td>
      <td>44155</td>
      <td>44300</td>
      <td>44300</td>
      <td>45243</td>
      <td>47695</td>
      <td>47300</td>
      <td>43595</td>
    </tr>
    <tr>
      <th>2019</th>
      <td>47300</td>
      <td>47300</td>
      <td>47195</td>
      <td>46477</td>
      <td>46000</td>
      <td>46000</td>
      <td>46000</td>
      <td>46000</td>
      <td>45437</td>
      <td>42975</td>
      <td>46000</td>
      <td>46000</td>
      <td>46108</td>
    </tr>
    <tr>
      <th>2020</th>
      <td>46000</td>
      <td>46000</td>
      <td>45900</td>
      <td>45800</td>
      <td>46068</td>
      <td>47000</td>
      <td>47352</td>
      <td>47725</td>
      <td>48100</td>
      <td>49292</td>
      <td>52400</td>
      <td>52600</td>
      <td>47823</td>
    </tr>
  </tbody>
</table>

### 4. 다년간의 농산물 월별 가격 변동 시각화

지면상의 문제로 이곳에는 그래프를 세개만 나타내었습니다.   
https://github.com/meatmaster-kyungfill/foodprice/blob/main/%EB%86%8D%EC%82%B0%EB%AC%BC%20%EC%9B%94%EB%B3%84%EC%8B%9C%EC%84%B8%20api(1996%EB%85%84~2020%EB%85%84).ipynb   
이곳에서는 1996년부터 ~2020년까지의 시세를 시각화 한것을 보실 수 있습니다.   
![image](https://user-images.githubusercontent.com/71205453/110238734-9198fd80-7f86-11eb-8ed7-a4b189920cc6.png)
![image](https://user-images.githubusercontent.com/71205453/110238763-c2793280-7f86-11eb-9884-bae9a986241c.png)
![image](https://user-images.githubusercontent.com/71205453/110238772-c9a04080-7f86-11eb-8bf1-5407815804d6.png)


### 5. 이 프로젝트는 아직 연구중   

예전 학교과제에서 적용했던 회귀분석 예측 모델을 이 프로젝트에서는 적용하지 않았습니다.   
왜냐하면 이 프로젝트에서는 머신러닝 모델을 적용을 해보고 싶었기 때문입니다.   
머신러닝 모델이 좀 더 익숙해지면 다시 프로젝트를 보완할 예정입니다.   
