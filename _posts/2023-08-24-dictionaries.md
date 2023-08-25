---
layout: post
title: Python Day9
subtitle: 딕셔너리 & 중첩 (Dictionaries & Nesting)
cover-img: /assets/img/20230824_dic10.png
thumbnail-img: /assets/img/20230824_dic10.png
share-img: /assets/img/20230824_dic10.png
tags: [python, day9, 딕셔너리, 중첩, Dictionaries, Nesting, 리스트, append, 비밀경매프로그램]
---
<br><br>

# 딕셔너리 & 중첩 (Dictionaries & Nesting)  
## Dictionaries  
- 실제 사전과 비슷하게 동작함  
- 관련된 정보들을 몇 개의 그룹으로 묶어줌  
- 모든 딕셔너리는 이렇게 두 부분으로 나뉨   

| Key | Value | 
| :------ |:--- | 
| Bug | An error in a program that prevents the problem from running as expected. | 
| Function | A piece of code that you can easily call over and over again. | 
| Loop | The action of doing something over and over again. |   

왼쪽은 Key 오른쪽은 이에 해당하는 값    

**1. 문법**
~~~
{key: Value}
~~~

<br>

 **2. 만약 딕셔너리에 하나 이상의 키와 값을 넣고 싶다면?**  
쉼표를 적어서 추가하면 됨  
~~~
{key1 : Value1 , key2 : Value2, key3 : Value3..}
~~~

<br>

**3. 읽기 쉽게 작성하는 법**  
![1](/assets/img/20230824_dic.png)

<br>

**4. 딕셔너리 불러오는 법**
~~~
programming_dictionary["bug"]
~~~

<br>

 **5. 딕셔너리 처음이 아닌 중간에 추가로 삽입하는 방법 + 수정할 때도 이 방법으로**  
![2](/assets/img/20230824_dic2.png)  


{: .box-note}
**Note:** 💡emplty_list=[ ]와 마찬가지로 빈 딕셔너리를 만들어 줄 수 있음.  
empty_dictionary={ }

<br>

**6. 딕셔너리를 통째로 지우고 싶을 때**  
![3](/assets/img/20230824_dic3.png)  

- 게임을 재시작해서 점수와 능력을 초기화 할 때와 같이 유저의 진행상황을 없애줘야 할 때 유용

<br>

**7. 딕셔너리로 반복문을 사용하는 방법**  
![4](/assets/img/20230824_dic4.png)  

<br>

### [인터렉티브 코딩 연습] 등급 매기는 프로그램  
![5](/assets/img/20230824_dic6.png)  

<br>

## Nesting (리스트와 딕셔너리 중첩하기)  
- 딕셔너리의 value값에 어떤 자료형이든 들어갈 수 있다.   
- 항상 key와 value 사이에 : 가 있어야 함  
![6](/assets/img/20230824_dic7.png)

<br>

### [인터렉티브 코딩 연습] 리스트 속 딕셔너리  
~~~
add_new_country("Russia", 2, ["Moscow", "Saint Petersburg"])  
추가로 넣어주려면?
~~~

1. 함수 생성하기(파라미터에 들어올 값들 이름 순서대로 설정)  
2. 빈 딕셔너리 만들어주기  
3. 각 파라미터 값 딕셔너리 value값으로 넣어주기    
{: .box-note}
**Note:** 💡 value값으로 넣어줬다는 건 결국 대괄호 안 이름은 key값이 됨.  
이 지점에서 print하면 value값만 나오지만, 딕셔너리에 넣어준 후에는 key와 value값이 모두 출력된다.  

4. append로 딕셔너리를 리스트 항목에 추가

<br>
     
![7](/assets/img/20230824_dic_8.png)

<br><br><br>  

## 비밀 경매 프로그램   
**Flowchart**  
![8](/assets/img/20230824_dic9.png)  

<br>

**코드작성**  
![10](/assets/img/20230824_dic11.png)  

1. 로고 import  
2. 이름, 입찰가 input 입력 받고 변수 생성(가격은 int type으로)  
3. 빈 딕셔너리 생성해서 이름과 입찰가를 딕셔너리에 추가하기  
(name을 key값으로, price를 value값으로 설정)  
4. while반복문을 생성해서 입찰할 다른 유저 여부 확인  
- 입찰이 끝났는지 확인하는 변수 생성(bidding_finished)  
- 입찰자 여부를 확인하는 if문 while문 안에 넣어주기  
5. yes일 경우 화면 초기화 clear()함수 사용  
6. no 일 경우 while문 false가 되서 높은 입찰가 책정하는 함수로 넘어가고 while문 빠져나옴  
7. 별도의 함수 생성  
💡파라미터명은 함수를 위해 작성 됐을 뿐 아규먼트값이 들어오면 대체됨 헷갈리지 말긔..  
- bidder에 아규먼트로 들어온 bids의 key값이 for반복문 각bidder에 할당됨  
- value값 변수명 붙여주기  
- if 문으로 가장 높은 값 찾기
 
![9](/assets/img/20230824_dic10.png)

<br>
 





