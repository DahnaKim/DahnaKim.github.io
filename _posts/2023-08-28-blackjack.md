---
layout: post
title: Python Day11
subtitle: 블랙잭 게임, Blackjack Capstone Project
cover-img: /assets/img/20230828_blackjack1.png
thumbnail-img: /assets/img/20230828_blackjack1.png
share-img: /assets/img/20230828_blackjack1.png
tags: [blackjack, capstone, flowchart, finalcode, python, day11, 파이썬, 블랙잭]
---
<br><br>

# Blackjack Capstone Project  

**캡스톤 프로젝트(Capstone Project)**  
지금까지 배운 지식과 기술을 종합하여 실제 문제에 적용하는 프로젝트  

<br>

### 블랙잭 룰  

- 가급적 21에 가까운 수를 얻어야 함
- 손에 쥔 카드가 21을 넘으면 안됨 (넘으면 Bust. 게임에서 졌다는 의미)
- 잭, 퀸, 킹이 있는 카드는 10으로 계산
- 에이스의 경우 합계를 고려해 1이나 11로 계산

<br> 

### Flow Chart  
![1](/assets/img/20230828_blackjack1.png)   

### Code  
1.  
![2](/assets/img/20230828_blackjack2.png)

2.  
![3](/assets/img/20230828_blackjack3.png)

3.  
![4](/assets/img/20230828_blackjack4.png)    

4.  
![5](/assets/img/20230828_blackjack5.png)

5.    
![6](/assets/img/20230828_blackjack6.png)

6.    
![7](/assets/img/20230828_blackjack7.png)
    
7.  
![8](/assets/img/20230828_blackjack8.png)

8.  
![9](/assets/img/20230828_blackjack9.png)

9.  
![10](/assets/img/20230828_blackjack10.png)

10.  
![11](/assets/img/20230828_blackjack11.png)

11.  
![12](/assets/img/20230828_blackjack12.png)     

<br><br>

## Final Code  
```javascript
import random
from replit import clear
from art import logo

def deal_card():
  cards = [11, 2, 3, 4, 5, 6, 7, 8, 9, 10, 10, 10, 10]
  card = random.choice(cards)
  return card

def calculate_score(cards):
  if sum(cards) == 21 and len(cards) == 2:
    return 0
  if 11 in cards and sum(cards) > 21:
    cards.remove(11)
    cards.append(1)
  
  return sum(cards)


def compare(user_score, computer_score):
  if user_score == computer_score:
    return "Draw"
  elif computer_score == 0:
    return "Lose, opponent has Blackjack"
  elif user_score == 0:
    return "Win with a Blackjack"
  elif user_score > 21:
    return "You went over. You lose"
  elif computer_score > 21:
    return "Opponent went over. You win"
  elif user_score > computer_score:
    return "You win"
  else:
    return "You lose"

def play_game():

  print(logo)
  
  user_cards = []
  computer_cards = []
  is_game_over = False
  
  for _ in range(2):
    user_cards.append(deal_card())
    computer_cards.append(deal_card())
  
  while not is_game_over:
    
    user_score = calculate_score(user_cards)
    computer_score = calculate_score(computer_cards)
    print(f" Your cards : {user_cards}, current score: {user_score}")
    print(f" Computer's first card: {computer_cards[0]}")
    
    if user_score == 0 or computer_score == 0 or user_score > 21:
      is_game_over = True
    else:
      user_should_deal = input("Type 'y' to get another card, type 'n' to pass: ")
      if user_should_deal == "y":
        user_cards.append(deal_card())
      else:
        is_game_over = True
  
  
  while computer_score != 0 and computer_score < 17:
    computer_cards.append(deal_card())
    computer_score = calculate_score(computer_cards)
  
  print(f" Your final hand: {user_cards}, final score: {user_score}")
  print(f" Computer's final hand: {computer_cards}, final score: {computer_score}")
  print(compare(user_score, computer_score))

while input("Do you want to play a game of Blackjack? Type 'y' or 'n': ") == "y":
  clear()
  play_game()

```
 
