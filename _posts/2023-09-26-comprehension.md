---
layout: post
title: Python Day25,26
subtitle: US States Quiz, List and Dictionary Comprehensions
cover-img: /assets/img/20230926_25_1.png
thumbnail-img: /assets/img/20230926_25_1.png
share-img: /assets/img/20230926_25_1.png
tags: [python, Day25, Day26, 미국 주 게임, US States Qiuz, Python Sequences, 시퀀스, Comprehensions, 컴프리헨션]
---

<br><br>
    
### 미국 주 게임 파트2 : CSV파일로 도전해 보기  
  
1️⃣ Pandas import 
  
<br>
  
2️⃣ pandas로 csv파일 읽고 변수에 저장하기  
  
```javascript
data = pandas.read_csv("50_states.csv")
```  
<br>  
  
3️⃣ 50_states.csv의 모든 주를 구하는 방법  
  
- state 시리즈를 가져와 리스트화   
<br>
  
4️⃣ if문으로 답이 리스트 안에 있는지 확인  
  
<br>  
  
5️⃣ 답이 50개 주 중의 하나이면 turtle생성  
  
<br>  
  
6️⃣ x, y 좌표 불러와 터틀 이동시키기  
  
- x,y 데이터 정수화
   
<br>  
  
7️⃣ 터틀이 위치에 도달하면 주 이름을 기록  
  
item()메소드를 활용하는 방법도 있음 - 기본 데이터의 첫 번째 요소를 가져오게 함  
  
<br>  
  
8️⃣ 정답을 맞출 때 마다 반복하게끔 반복문  
  
- 빈 리스트를 만들어 추가되고 len 함수를 사용해 while문 조건으로 만들기
   
<br>  
  
9️⃣ 입력창의 제목 바꾸기  
  
- 맞춘 주의 숫자 넣기
   
<br>  
  
🔟 대소문자 구분 없이 작동하게 하기  
  
title()메소드 활용 - 첫글자를 대문자로 바꿔줌  
  
![1](/assets/img/20230926_25_1.png)  
  
<br><br>  
  
### 미국 주 게임 파트3 : CSV파일에 저장하기  
  
**학습 도구로 게임 활용하기**  
  
1️⃣ exit 코드를 입력해서 게임을 종료  
  
- break로 while문 종료
    
- 맞추지 못한 주를 for반복문을 돌려 확인하고, 따로 리스트로 만들기

   <br>
  
2️⃣ 기록 파일 만들기  
  
- pandas를 이용해 데이터프레임으로 만들기
   
- csv파일로 생성
    
![2](/assets/img/20230926_25_2.png)  

<br><br>  
    
### Final Code  
  
```javascript
import turtle
import pandas


screen = turtle.Screen()
screen.title("U.S. States Game")
image = "blank_states_img.gif"
screen.addshape(image)
turtle.shape(image)

data = pandas.read_csv("50_states.csv")
all_states = data.state.to_list()
guessed_states = []

while len(guessed_states) < 50:
    answer_state = screen.textinput(title=f"{len(guessed_states)}/50 States Correct",
                                    prompt="What's another state's name?").title()
    if answer_state == "Exit":
        missing_states = []
        for state in all_states:
            if state not in guessed_states:
                missing_states.append(state)
        new_data = pandas.DataFrame(missing_states)
        new_data.to_csv("states_to_learn.csv")
        break
    if answer_state in all_states:
        guessed_states.append(answer_state)
        t = turtle.Turtle()
        t.hideturtle()
        t.penup()
        state_data = data[data.state == answer_state]
        t.goto(int(state_data.x), int(state_data.y))
        t.write(answer_state)
        #t.write(state_data.state.item())

turtle.mainloop()
```
  <br><br>

# Day26  
  
## List and Dictionary Comprehensions  
  
### List Comprehension  
  
- 파이썬에 있는 독특한 특징 중 하나
   
- 입력할 양을 줄여주고 코드를 훨씬 더 짧게 쓸 수 있다.
   
- 가독성이 좋음
   

![3](/assets/img/20230926_25_3.png)  
<br>
  
![4](/assets/img/20230926_25_4.png)  
  

- 리스트가 아닌 다른 시퀀스로도 작업할 수 있음
  
  <br>
    
**Python Sequences**  
  
명확하게 순서를 갖고 있음  
- list  
- range  
- string  
- tuple

  <br>
  
**조건이 포함된 리스트 컴프리헨션**  
  
![5](/assets/img/20230926_25_5.png)  

  <br><br>
  
### List Comprehension 1 Exercise  
  
**리스트의 숫자 각각 제곱수로 변환해 리스트로 만들기**  
  
![6](/assets/img/20230926_25_6.png)  

  <br><br>
     

### List Comprehension 2 Exercise  
  
**리스트에서 짝수인 수만 새로운 리스트로 만들기**  
  
![7](/assets/img/20230926_25_7.png)  

<br>
  
### List Comprehension 3 Exercise   
  
**두 파일의 교집합 숫자를 리스트로 만들기**  
  
![8](/assets/img/20230926_25_8.png)  
  
<br>
  
### 미국 주 게임에 List 컴프리헨션 적용  
  
![9](/assets/img/20230926_25_9.png)  

  <br>
  
### Dictionary Comprehension  
  
```javascript
기본 형태
new_dict = {new_key:new_value for item in list}

이미 존재하는 딕셔너리에 있는 값으로 새로운 딕셔너리 생성
new_dict = {new_key:new_value for (key, value) in dict.items() if test}
```

<br>   
  
**예시**  
   
![10](/assets/img/20230926_25_10.png)  

  <br>
