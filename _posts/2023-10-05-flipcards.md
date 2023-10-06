---
layout: post
title: Python Day31
subtitle: Capstone Project - Flash Card Program
cover-img: /assets/img/20231005_31_3.png
thumbnail-img: /assets/img/20231005_31_3.png
share-img: /assets/img/20231005_31_3.png
tags: [python, Day31, Flash Card Program, 플래시 카드 프로그램]
---

<br><br>
  
 # Capstone Project - Flash Card Program  
  
### UI 만들기  
  
1️⃣ 윈도우 구성  
  
![1](/assets/img/20231005_31_1.png)  
  
<br>
  
2️⃣ 카드 앞면 이미지 넣기  
  
![2](/assets/img/20231005_31_2.png)  
  
<br>
  
3️⃣ 텍스트, 버튼 넣기  
  
![3](/assets/img/20231005_31_3.png)  
  
<br><br>
  

### 새 플래시 카드 만들기  
  
1️⃣ 버튼에 호출 될 함수 생성  
  
<br>
  
2️⃣ csv파일에서 단어를 가져와 번역된 단어 찾기  
1) import pandas   
2) pandas.read_csv  
3) data 변수에 저장  
4) 딕셔너리로 변환  
(orient="records")를 넣어줘서 다른 형태로 변환
  
~~~
🐤기존 형태 
{'French':{0:'partie'}},{'English':{0:'part'}}

🐤(orient="records")적용
[{'French':'partie'},{'English':'part'}]
~~~

<br>
  
3️⃣ 랜덤으로 리스트의 단어 뽑기  
  
<br>
  
4️⃣ 뽑은 단어 캔버스에 넣기  
- text와 word 코드 변수 선언  
- 함수에 canvas.itemconfig 사용해서 변경
  
<br>
  
5️⃣ 함수 호출  
  
![4](/assets/img/20231005_31_4.png)  
  
<br>
  
### 카드 뒤집기  
  
1️⃣ window.after 메소드 사용    
<br>
2️⃣ flip_card함수 생성  
<br>
3️⃣ 빈 딕셔너리 생성해서 랜덤으로 생성된 current_card["English"]구하기  
<br>
4️⃣ 이미지 변경하기, 텍스트 컬러 변경하기  
<br>
5️⃣ 카드 뒷면에서 버튼 클릭으로 다시 앞면으로 돌아왔을 때 구성 설정  
<br>
6️⃣ 카드가 뒤집히는 매커니즘 설정  
<br>
7️⃣ 버튼 여러번 클릭시 다른 단어로 넘어가는 도중 3초 후 카드가 뒤집히는 버그 수정  
- 타이머 전역변수선언  
- 버튼 중 하나를 클릭했을 때 타이머 무효화  
- 다시 타이머 설정  
⇨ 버튼 누르면 함수 호출되면서 타이머 꺼지고 랜덤카드 뽑은 후 타이머 켜짐
  
![5](/assets/img/20231005_31_5.png)  
  
<br><br>
  
### 데이터 저장하기   
  
1️⃣ 체크마크를 누른 단어는 다시 안보이게 설정  
- 체크마크를 누르면 to_learn리스트에서 current_card를 제거하는 함수 생성
  
<br> 
  
2️⃣ 영구 파일로 저장하기    
<br>
3️⃣ 저장한 csv파일 읽기  
- words_to_learn.csv파일을 지웠을 때 나타나는 오류 예외처리  
<br>
4️⃣ pandas가 데이터프레임 생성시 record번호 붙이는 오류 수정  
  
![6](/assets/img/20231005_31_6.png)  
  
![7](/assets/img/20231005_31_7.png)  

<br><br>

### Final Code

```javascript
from tkinter import *
import pandas
import random

BACKGROUND_COLOR = "#B1DDC6"
current_card = {}
to_learn = {}

try:
    data = pandas.read_csv("data/words_to_learn.csv")
except FileNotFoundError:
    original_data = pandas.read_csv("data/french_words.csv")
    to_learn = original_data.to_dict(orient="records")
else:
    to_learn = data.to_dict(orient="records")


def next_card():
    global current_card, flip_timer
    window.after_cancel(flip_timer)
    current_card = random.choice(to_learn)
    canvas.itemconfig(card_title, text="French", fill="black")
    canvas.itemconfig(card_word, text=current_card["French"], fill="black")
    canvas.itemconfig(card_background, image=card_front_img)
    flip_timer = window.after(3000, func=flip_card)


def flip_card():
    canvas.itemconfig(card_title, text="English", fill="white")
    canvas.itemconfig(card_word, text=current_card["English"], fill="white")
    canvas.itemconfig(card_background, image=card_back_img)


def is_known():
    to_learn.remove(current_card)
    data = pandas.DataFrame(to_learn)
    data.to_csv("data/words_to_learn.csv", index=False)

    next_card()


window = Tk()
window.title("Flashy")
window.config(padx=50, pady=50, bg=BACKGROUND_COLOR)

flip_timer = window.after(3000, func=flip_card)

canvas = Canvas(width=800, height=526)
card_front_img = PhotoImage(file="images/card_front.png")
card_back_img = PhotoImage(file="images/card_back.png")
card_background = canvas.create_image(400, 263, image=card_front_img)
card_title = canvas.create_text(400, 150, text="", font=("Ariel", 40, "italic"))
card_word = canvas.create_text(400, 263, text="", font=("Ariel", 60, "bold"))
canvas.config(bg=BACKGROUND_COLOR, highlightthickness=0)
canvas.grid(row=0, column=0, columnspan=2)

cross_image = PhotoImage(file="images/wrong.png")
unknown_button = Button(image=cross_image, highlightthickness=0, borderwidth=0, command=next_card)
unknown_button.grid(row=1, column=0)

check_image = PhotoImage(file="images/right.png")
known_button = Button(image=check_image, highlightthickness=0, borderwidth=0, command=is_known)
known_button.grid(row=1, column=1)

next_card()


window.mainloop()
```
<br><br>

<video width="320" height="240" controls>
 <source src="/assets/img/20231005_31_1.mp4" type="video/mp4">
</video>
