---
layout: post
title: Python Day36
subtitle: Stock News Monitoring Project
cover-img: /assets/img/20231012_36_2.png
thumbnail-img: /assets/img/20231012_36_2.png
share-img: /assets/img/20231012_36_2.png
tags: [Day36, Stock News, 주식 뉴스 알림, items(), abs(), 절대값, API]
---
  
<br><br>
    
# Stock News Monitoring Project  
  
### 주가 변동 확인하기  
  
1️⃣ endpoint, stock, company name, API Key 생성 후 상수로 저장  
  
2️⃣ import requests 모듈, requests메소드 이용해서 파라미터, response 생성  
  
![1](/assets/img/20231012_36_1.png)  

  <br>

3️⃣어제 종가 구하기  
  
- 날짜 딕셔너리는 계속 변경하기 때문에 리스트 컴프리헨션을 사용해 접근할 수 있도록 변경  
  
~~~ 
💡items()메소드는 딕셔너리에서 키와 값을 튜플 형태로 반환해줌
⇨ [("a", 1), ("b", 2), ("c", 3)]
~~~
  
![2](/assets/img/20231012_36_2.png) 

<br>
  
4️⃣ 그저께 종가 구하기  
  
![3](/assets/img/20231012_36_3.png)  

<br>
  
5️⃣ 어제와 그제 종가 비교  
  
~~~
**Python abs() Function**
숫자의 절대값을 리턴하는 함수
숫자 앞에 있는 모든 음수 표시를 제거
~~~
  
![4](/assets/img/20231012_36_4.png)  

<br>
 
6️⃣ 종가 차이 비율 구하기   
  
![5](/assets/img/20231012_36_5.png)  

<br>
  
7️⃣ 차이가 4%이상이면 print("Get News")  
  
```javascript
if diff_percent > 4:
    print("Get News")
```

<br><br>

### 뉴스 기사 가져오기  
  
1️⃣ news API Key 상수로 저장, requests메소드 이용해서 파라미터, response 생성  
  
2️⃣ 키를 넣어서 관련 키워드의 모든 기사 잡기  
  
![6](/assets/img/20231012_36_6.png)  
  
<br>
  
3️⃣slice()를 이용해서 처음 3개의 기사만 얻기  
  
![7](/assets/img/20231012_36_7.png)  

<br><br>

### SMS 메시지 보내기  
  
1️⃣ 컴프리헨션으로 첫 기사 3개의 제목과 요약문으로 된 리스트 만들기  
  
![8](/assets/img/20231012_36_8.png)  

<br>

2️⃣ twilio를 통해 메시지 전송  
  
- import, sid, token 저장
   
![9](/assets/img/20231012_36_9.png)  

<br>
  
- Client클래스로부터 내 클라이언트 생성해서 설정  
- 반복문으로 세 개의 메시지 전송
   
![10](/assets/img/20231012_36_10.png)  

<br>

3️⃣ 주식이 올랐는지 내렸는지 보여주기  
  
![11](/assets/img/20231012_36_11.png)  

<br><br>

### Final Code  
```javascript
import requests
from twilio.rest import Client

STOCK_NAME = "TSLA"
COMPANY_NAME = "Tesla Inc"

STOCK_ENDPOINT = "https://www.alphavantage.co/query"
NEWS_ENDPOINT = "https://newsapi.org/v2/everything"

STOCK_API_KEY = ""
NEWS_API_KEY = ""
TWILIO_SID = ""
TWILIO_AUTH_TOKEN = ""

stock_params = {
    "function": "TIME_SERIES_DAILY",
    "symbol": STOCK_NAME,
    "apikey": STOCK_API_KEY,
}

response = requests.get(STOCK_ENDPOINT, params=stock_params)
data = response.json()["Time Series (Daily)"]
data_list = [value for (key, value) in data.items()]
yesterday_data = data_list[0]
yesterday_closing_price = yesterday_data["4. close"]
print(yesterday_closing_price)

day_before_yesterday_data = data_list[1]
day_before_yesterday_closing_price = day_before_yesterday_data["4. close"]
print(day_before_yesterday_closing_price)

difference = float(yesterday_closing_price) - float(day_before_yesterday_closing_price)
up_down = None
if difference > 0:
    up_down = "📈"
else:
    up_down = "📉"


diff_percent = round((difference / float(yesterday_closing_price)) * 100, 2)
print(diff_percent)

if abs(diff_percent) > 1:
    news_params = {
        "apiKey": NEWS_API_KEY,
        "qInTitle": COMPANY_NAME,
    }

    news_response = requests.get(NEWS_ENDPOINT, params=news_params)
    articles = news_response.json()["articles"]

    three_articles = articles[:3]
    print(three_articles)

    formatted_articles = [f"{STOCK_NAME}: {up_down}{diff_percent}%\nHeadline: {article['title']}. \nBrief: {article['description']}"
                          for article in three_articles]

    client = Client(TWILIO_SID, TWILIO_AUTH_TOKEN)

    for article in formatted_articles:
        message = client.messages.create(
            body=article,
            from_="",
            to=""
        )

```

