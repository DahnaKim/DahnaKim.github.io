---
layout: post
title: Python Day37
subtitle: Advanced Authentication and POST PUT DELETE Requests
cover-img: /assets/img/20231013_37_1.png
thumbnail-img: /assets/img/20231013_37_1.png
share-img: /assets/img/20231013_37_1.png
tags: [Day37, POST PUT DELETE Requests, 습관 추적기, habit tracker, 매개변수 json params, Request Header, strftime(), 날짜자동채우기]
---
    
<br><br>
      
# Advanced Authentication and POST / PUT / DELETE Requests  
  
### HTTP Post Requests  
  
- GET : API 제공자 같이 외부 시스템에 특정한 데이터를 요청할 때  
- POST : 우리가 외부 시스템에 어떤 데이터를 주고 성공여부를 제외하고는 시스템으로부터 받는 응답에는 관심X  
- PUT : 외부 서비스에서 단순히 데이터를 업데이트 하는 것  
- DELETE : 외부 데이터에 있는 데이터를 삭제할 때

<br><br>

## pixela API를 이용해 습관 추적기 구축  
  
### 계정 생성  
  
[pixela API 사이트](https://pixe.la)  
  
1️⃣ import requests, url endpoint 변수 저장  
  
2️⃣ post요청  
- 필수 매개변수 넣어주기
   
![1](/assets/img/20231013_37_1.png)  

<br>
  
- JSON으로 써야 하는 이유
   
![2](/assets/img/20231013_37_2.png)  

<br>

![3](/assets/img/20231013_37_3.png) 

<br><br>

### HTTP 헤더를 이용한 고급 인증  
  
**Request Header란**  
  
![4](/assets/img/20231013_37_4.png)  

<br>

- HTTP 헤더를 권장하는 이유 : API키가 로그나 요청 스니핑에서 타인에게 보이지 않게 하기 위함
   
![5](/assets/img/20231013_37_5.png)  

<br>

- 웹 브라우저에 생성됨(주소 마지막에 html붙이기)
  
~~~
https://pixe.la/v1/users/<username>/graphs/<graphID>.html
~~~

  
![6](/assets/img/20231013_37_6.png)  

<br><br>

### Post Request로 습관 추적기에 픽셀 추가하기  
  
![7](/assets/img/20231013_37_7.png)  

<br>

![8](/assets/img/20231013_37_8.png)  

<br>

### strftime으로 자동으로 오늘 날짜 채우기  
  
1️⃣ import datetime  
  
2️⃣ 오늘 날짜 받기, strftime으로 원하는 형식으로 바꾸기  
  
[Python Datetime document](https://www.w3schools.com/python/python_datetime.asp)  
  
![9](/assets/img/20231013_37_9.png)  

<br><br>

### HTTP PUT및 DELETE Requests 사용법  
  
- PUT  
  
![10](/assets/img/20231013_37_10.png)

<br>

- DELETE
   
![11](/assets/img/20231013_37_11.png)  

<br><br>

### Final Code

```javascript
import requests
from datetime import datetime

USERNAME = "dahna0915"
TOKEN = ""
GRAPH_ID = "graph1"

pixela_endpoint = "https://pixe.la/v1/users"

user_params = {
    "token": TOKEN,
    "username": USERNAME,
    "agreeTermsOfService": "yes",
    "notMinor": "yes"
}

# response = requests.post(pixela_endpoint, json=user_params)

graph_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs"

graph_config = {
    "id": GRAPH_ID,
    "name": "Cycling Graph",
    "unit": "Km",
    "type": "float",
    "color": "ajisai"
}

headers = {
    "X-USER-TOKEN": TOKEN
}

# response = requests.post(url=graph_endpoint, json=graph_config, headers=headers)
# print(response.text)

pixel_creation_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs/{GRAPH_ID}"

today = datetime.now()

pixel_data = {
    "date": today.strftime("%Y%m%d"),
    "quantity": input("How many kilometers did you cycle today? "),
}

response = requests.post(url=pixel_creation_endpoint, json=pixel_data, headers=headers)
print(response.text)

update_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs/{GRAPH_ID}/{today.strftime('%Y%m%d')}"

new_pixel_data = {
    "quantity": "4.5"
}

# response = requests.put(url=update_endpoint, json=new_pixel_data, headers=headers)
# print(response.text)

delete_endpoint = f"{pixela_endpoint}/{USERNAME}/graphs/{GRAPH_ID}/{today.strftime('%Y%m%d')}"

# response = requests.delete(url=delete_endpoint, headers=headers)
# print(response.text)
```


