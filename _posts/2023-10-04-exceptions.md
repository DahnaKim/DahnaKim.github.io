---
layout: post
title: Python Day30
subtitle: Errors, Exceptions and Saving JSON Data
cover-img: /assets/img/20231004_30_2.png
thumbnail-img: /assets/img/20231004_30_2.png
share-img: /assets/img/20231004_30_2.png
tags: [python, Day30, 예외처리, Errors, Exceptions, JSON, NATO 음성 알파벳 프로젝트의 예외 처리, Password Manager JSON 예외처리 적용]
---

<br><br>
    
# Errors, Exceptions and Saving JSON Data  
  
### Handling Errors & Exceptions  
  
**Error 종류**  
  
![1](/assets/img/20231004_30_1.png)  
  
- try : 예외를 유발할 수 있는 코드 블록  
  
- except : 만약 예외가 있다면 컴퓨터가 실행하게 하려는 블록  
  
- else : 예외가 없었을 때 실행할 코드를 정의  
  
- finally : 어떤 일이 일어나더라도 실행해야 할 코드   
  
![2](/assets/img/20231004_30_2.png)  

<br><br>  
### Raising Exceptions : 나만의 예외 생성하기  
  
- raise : 자신만의 예외를 생성할 수 있음
   
![3](/assets/img/20231004_30_3.png)  

<br>
  
### KeyError Handling Exercise  
  
![4](/assets/img/20231004_30_4.png)  

<br> 
  
### 코드 예제 : NATO 음성 알파벳 프로젝트의 예외 처리  
  
![5](/assets/img/20231004_30_5.png)  
  
<br><br>
  
### Password Manager에서 JSON 데이터 읽고 쓰고 업데이트하기  
  
**JSON(JavaScript Object Notation)**  
  
- 자바스크립트를 위해 설계됐음
- 구조가 단순해서 이해하고 다루기 쉬워 많은 분야에서 채택됨
- 가장 널리 사용되는 데이터 전송 방법
- 특히 인터넷을 통해 데이터를 전송할 때 많이 씀
- 본질적으로 네스티드 리스트와 딕셔너리들로 구성되어 있음
- 키 값 쌍 데이터 구조를 갖고 있음
- 내장된 JSON 라이브러리를 이용
- Write : json.dump()
- Read : json.load()
- Update : json.update()

<br>
  
**JSON 데이터 입력**  
  
![6](/assets/img/20231004_30_6.png)  

<br>
  
**JSON 데이터 읽기**  
  
![7](/assets/img/20231004_30_7.png)  
  
<br>
  
**JSON 데이터 업데이트**  
  
![8](/assets/img/20231004_30_8.png)  
  
![9](/assets/img/20231004_30_9.png)  
  
<br>
  
### Password Manager에서 예외처리하기  
  
![10](/assets/img/20231004_30_10.png)  
  
<br>  
  
### 패스워드 매니저에서 웹사이트 검색하기  
  
- 버튼 생성
  
```javascript
search_button = Button(text="Search", width=13, command=find_password)
```
  
<br>
   
![11](/assets/img/20231004_30_11.png)  
  
<br>
  
### Final Code
```javascript
from tkinter import *
from tkinter import messagebox
from random import choice, randint, shuffle
import pyperclip
import json
# ---------------------------- PASSWORD GENERATOR ------------------------------- #

def generate_password():
    letters = ['a', 'b', 'c', 'd', 'e', 'f', 'g', 'h', 'i', 'j', 'k', 'l', 'm', 'n', 'o', 'p', 'q', 'r', 's', 't', 'u', 'v', 'w', 'x', 'y', 'z', 'A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']
    numbers = ['0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
    symbols = ['!', '#', '$', '%', '&', '(', ')', '*', '+']

    password_letters = [choice(letters) for _ in range(randint(8, 10))]
    password_symbols = [choice(symbols) for _ in range(randint(2, 4))]
    password_numbers = [choice(numbers) for _ in range(randint(2, 4))]

    password_list = password_letters + password_symbols + password_numbers
    shuffle(password_list)

    password = "".join(password_list)
    password_entry.insert(0, password)
    pyperclip.copy(password)
    messagebox.showinfo(title="Message", message="The password has been created and copied.")


# ---------------------------- SAVE PASSWORD ------------------------------- #
def save():
    website = website_entry.get()
    email = email_entry.get()
    password = password_entry.get()
    new_data = {
        website: {
            "email": email,
            "password": password,
        }
    }

    if len(website) == 0 or len(password) == 0:
        messagebox.showinfo(title="Oops", message="Please make sure you haven't left any fields empty.")
    else:
        try:
            with open("data.json", "r") as data_file:
                #Read old data
                data = json.load(data_file)
        except FileNotFoundError:
            with open("data.json", "w") as data_file:
                json.dump(new_data, data_file, indent=4)
        else:
            #Updating old data with new data
            data.update(new_data)

            with open("data.json", "w") as data_file:
                #Saving updated data
                json.dump(data, data_file, indent=4)
        finally:
            website_entry.delete(0, END)
            password_entry.delete(0, END)

# ---------------------------- FIND PASSWORD ------------------------------- #
def find_password():
    website = website_entry.get()
    try:
        with open("data.json") as data_file:
            data = json.load(data_file)
    except FileNotFoundError:
        messagebox.showinfo(title="Error", message="No Data File Found.")
    else:
        if website in data:
            email = data[website]["email"]
            password = data[website]["password"]
            messagebox.showinfo(title=website, message=f"Email: {email}\nPassword: {password}")
        else:
            messagebox.showinfo(title="Error", message=f"No details for {website} exists.")






# ---------------------------- UI SETUP ------------------------------- #

window = Tk()
window.title("Password Manager")
window.config(padx=50, pady=50)

canvas = Canvas(height=200, width=200)
logo_img = PhotoImage(file="logo.png")
canvas.create_image(100, 100, image=logo_img)
canvas.grid(row=0, column=0, columnspan=3)  # Center the canvas by spanning 2 columns

# Labels
website_label = Label(text="Website:")
website_label.grid(row=1, column=0)
email_label = Label(text="Email/Username:")
email_label.grid(row=2, column=0)
password_label = Label(text="Password:")
password_label.grid(row=3, column=0)

# Entries
website_entry = Entry(width=21)  # Set width to 36
website_entry.grid(row=1, column=1)
website_entry.focus()
email_entry = Entry(width=38)  # Set width to 36
email_entry.grid(row=2, column=1, columnspan=2)
email_entry.insert(0, "dahna0915@gmail.com")
password_entry = Entry(width=21)
password_entry.grid(row=3, column=1)

# Buttons
search_button = Button(text="Search", width=13, command=find_password)
search_button.grid(row=1, column=2)
generate_password_button = Button(text="Generate Password", command=generate_password)
generate_password_button.grid(row=3, column=2)
add_button = Button(text="Add", width=36, command=save)
add_button.grid(row=4, column=1, columnspan=2)

window.mainloop()
```
