---
layout: post
title: Python Day13
subtitle: Debugging
cover-img: /assets/img/20230831_steve.jpg
thumbnail-img: /assets/img/20230831_steve.jpg
share-img: /assets/img/20230831_steve.jpg
tags: [debugging,디버깅,파이썬,python, day13]
---
<br><br>

# Debugging🪲  
### Reproduce the Bug  

![1](/assets/img/20230831_debugging.png)  

randint는 a와 b 사이의 정수를 무작위로 반환함(양쪽 끝의 값도 포함)  
리스트는 0부터 세기 때문에 범위를 (0,5)로 수정해야 함  

**수정된 코드**  

~~~
from random import randint
dice_imgs = ["❶", "❷", "❸", "❹", "❺", "❻"]
dice_num = randint(0, 5)
print(dice_imgs[dice_num])
~~~

<br>

### 컴퓨터 입장에서 생각해보기  

![2](/assets/img/20230831_debugging2.png)  

1994년생이 포함되지 않음  

**수정된 코드**  

~~~
year = int(input("What's your year of birth?"))
if year > 1980 and year < 1994:
  print("You are a millenial.")
elif year >= 1994:
  print("You are a Gen Z.")
~~~

<br>

### Fix the Errors  

![3](/assets/img/20230831_debugging3.png)  

- age를 int 타입으로 바꿔야 함  
-if문 안의 조건 들여쓰기 + f-string으로 써주기  

**f-string(formatted string literals)**  
f-string은 파이썬 3.6부터 도입된 문자열 포매팅 방법으로, 문자열 내에 변수나 표현식의 값을 직접 삽입할 수 있게 해줌  

**수정된 코드**  

~~~
age = int(input("How old are you?"))
if age > 18:
  print(f" You can drive at age {age}.")
~~~

<br>

### print()구문으로 버그찾기  

![4](/assets/img/20230831_debugging4.png)  

<br>

### Use a Debugger  

**디버거 사용하기**  
- Thonny  
- [웹 버전 python tutor](https://pythontutor.com/visualize.html#mode=edit)

<br>

### Debugging: Final Tips  
- 휴식.. 차 마시거나 눈 붙여랔  
- 해도해도 모르면 주변 사람들에게 물어봐라  
- 코드를 자주 실행해봐라  
- 스택 오버플로우 사이트 활용

<br> 

### 실수를 두려워하지 않기!  

![5](/assets/img/20230831_steve.jpg)  
