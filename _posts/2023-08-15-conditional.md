---
layout: post
title: Python Day3
subtitle: if else문, else if문, 논리연산자, 코드블록, 범위, 전역과 지역, 이름공간 등..
cover-img: /assets/img/20230815_logic.png
thumbnail-img: /assets/img/20230815_logic.png
share-img: /assets/img/20230815_logic.png
tags: [python, day3, 조건문, if, else, 논리연산자, elif, 비교연산]
---

**요약**
- 조건문 (conditional)
- if else문, else if문, 논리연산자, 코드블록, 범위, 전역과 지역, 이름공간 등..  
🐧 중첩if : A조건 충족된 그룹 B조건으로 넘어감  
🐦 elif : A조건 충족 안되면 A-2조건으로 넘어감  
🐤 다중if : A조건 충족된 그룹 B, B-2  

### if/else. 
특정 조건에 따라 A나 B를 수행

- if와 else 각각 콜론 : 붙여주기
- 들여쓰기 주의
  
```javascript
ex)  
height = int(input("What is your height in cm?"))  
if height > 120 :  
   print("You can ride the rollercoaster!")  
else :  
   print("Sorry, you have to grow taller before you can ride.")  
```
### 비교 연산자 (Comparison Operators)
> : Greater than  
< : Less than  
<= : Greater than or equal to  
>= : Less than or equal to  
== : Equal to ( = 하나만 써 줄때는 값을 변수로 지정해준다는 의미임 )  
!= : Not equal to  
<br><br>
🐶 **과제 Odd or Even (홀수 또는 짝수)**  
% (모듈로) : 나누기 후 나머지를 보여줌
> 
![10](/assets/img/20230815_even.png)  

자바 수업 때 했던 거라 간단하게 패스  
<br><br>
### 중첩 if문(Nested if / else)  
```javascript
ex)
height = int(input("What is your height in cm?"))

if height > 120 :
   print("You can ride the rollercoaster!")
   age = int(input("What is your age?"))
   if age <= 18 :
      print("Please pay $7.")
   else :
      print("Please pay $12.")
else :
   print("Sorry, you have to grow taller before you can ride.")
```
<br><br>
### elif문
조건을 원하는 만큼 많이 추가할 수 있음  
if문에서 참이 아닐 경우, elif문을 쓰면 이어서 계속 참인지 확인   
```javascript
ex)
height = int(input("What is your height in cm?"))

if height > 120 :
   print("You can ride the rollercoaster!")
   age = int(input("What is your age?"))
   if age < 12 :  # 11살까지는 체크가 된 상태. 참이 아닌 경우 다음 elif문으로 넘어감
     print("Please pay $5.")
   elif age <= 18 : # 12살 이상 18살 이하
      print("Please pay $7.")
   else : 
      print("Please pay $12.")
else :
   print("Sorry, you have to grow taller before you can ride.")
```

🐰 **BMI계산기 ver.2..**  
![9](/assets/img/20230815_bmi2.png)
<br><br>

🐯 **코딩 연습 윤년(Leap Year Exercise)**
![8](/assets/img/20230815_logic.png)
순서도를 짜서 시각화 시키면 코드로 변환하기 훨씬 쉬워짐
![7](/assets/img/20230815_leap.png)
<br><br>
### Multiple if
다수의 조건이 있어 앞의 조건이 참이어도 여러 조건을 확인해야 하는 경우  
(앞서 if / elif / else는 하나의 결과만 수행이 되지만 다중 연속 if는 여러 조건이 참이면 여러 결과 수행)
![6](/assets/img/20230815_flowcha.png)
![5](/assets/img/20230815_bill.png)
아무것도 수행 안해도 되면 else 안써도 됨  
⭐️들여쓰기가 매우 중요함 같은 단계에 있는 조건 같은 라인에.⭐️  
<br><br>
**피자 주문 실습**
![4](/assets/img/20230815_pizza.png)
<br><br>
### 논리 연산자 (Logical Operators)
서로 다른 조건들을 결합하여 같은 행의 코드에 알려줌  

- A and B : 둘 다 참이어야 함  
- C or D : 하나만 참이어도 True  
- not E : 	조건에 반대로 결과를 만듦  
![3](/assets/img/20230815_logical.png)
<br><br>
**사랑계산기**
![2](/assets/img/20230815_cal1.png)
![lovecal](/assets/img/20230815_lovecal.png)


