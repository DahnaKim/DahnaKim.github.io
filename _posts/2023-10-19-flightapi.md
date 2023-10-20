---
layout: post
title: Python Day39, Day40
subtitle: CAPSTONE Part2 - The Flight Club
cover-img: /assets/img/20231019_40_4.png
thumbnail-img: /assets/img/20231019_40_4.png
share-img: /assets/img/20231019_40_4.png
tags: [Day39, Day40, 항공권, Cheap Flight Finder, Sheety, OOP, API, smtplib, 구글시트, SMS, 메일전송]
---
    
<br><br>
 
### 항공권 가격이 구글시트에 있는 가격보다 저렴하면 SMS전송  
  
- Twilio를 사용하여 SMS 전송하기   
  
1️⃣ notification_manager.py생성  
  
![1](/assets/img/20231019_40_1.png)  

<br>
  
2️⃣ main.py에서 조건문 생성  
  
![2](/assets/img/20231019_40_2.png)  

<br><br>
  
# CAPSTONE Part2 - The Flight Club  
  
### 고객 등록 코드 만들기  
  
- 새 리플잇 프로젝트 생성  
- 구글 시트에서 새 탭 생성  
- 성, 이름, 이메일 열 추가  
- Sheety에 새로운 시트 등록(POST체크)  
  
![3](/assets/img/20231019_40_3.png)  

<br><br>
  
### 항공편이 없는 도착지 예외처리, 직항편이 없는 도착지
  
- 항공권이 검색되지 않으면 1회 경유하는 항공권이 있는지 확인
   
![4](/assets/img/20231019_40_4.png)  

<br>
  
- FlightData클래스를 수정, 파라미터 옵션 추가
   
![5](/assets/img/20231019_40_5.png)  

<br>
  
- main.py 수정
   
![6](/assets/img/20231019_40_6.png)  

<br><br>
  
### 전체 고객에게 이메일 보내기  
  
- NotificationManager안에 send_emails()메소드 생성
   
※ 기호를 넣으면 오류가 발생할 수 있음  
  
[UTF-8로 인코딩해서 해결](https://stackoverflow.com/questions/9942594/unicodeencodeerror-ascii-codec-cant-encode-character-u-xa0-in-position-20#answer-9942885)
  
![7](/assets/img/20231019_40_7.png)  

<br>

**오류의 늪...**
![8](/assets/img/20231019_40_8.png)  
<br>
![10](/assets/img/20231019_40_10.png)  
<br>
![9](/assets/img/20231019_40_9.png)  
  
