---
layout: post
title: Python Day51, Day52
subtitle: Complaining Bot, Instagram Follower Bot
cover-img: /assets/img/20231108_51_2.png
thumbnail-img: /assets/img/20231108_51_2.png
share-img: /assets/img/20231108_51_2.png
tags: [Day51, Day52, execute_script(), selenium, 셀레늄, instagram follow, ChromeDriverManager().install()]
---
      
<br><br>

# Complaining Twitter Bot  
  
<br>  
  
![1](/assets/img/20231108_51_1.png)  

<br>

- execute_script()
Python (또는 다른 언어의 셀레늄 바인딩을 사용하는 경우)에서 직접 JavaScript 코드를 실행할 수 있게 해줌   
웹 페이지가 로드된 브라우저 컨텍스트 내에서 실행되기 때문에, 페이지에 존재하는 요소를 조작하거나, 페이지의 상태를 검사하거나, 사용자 정의 스크립트를 실행하는 데 유용  

**execute_script() 메서드는 두 가지 주요 매개변수를 받는다**  
script: 실행할 JavaScript 코드를 문자열로 전달합니다.  
*args: JavaScript 코드 내에서 사용할 인자들을 전달   
이 인자들은 JavaScript 코드 내에서 arguments[0], arguments[1], arguments[n] 등으로 접근할 수 있다.  
  
![2](/assets/img/20231108_51_2.png)

<br><br>

# Instagram Follower Bot
<br>
- ChromeDriverManager().install()
사용자의 운영체제와 크롬 브라우저 버전에 맞는 ChromeDriver의 최신 버전을 찾아서, 
필요한 경우 다운로드하고, 해당 드라이버의 경로를 반환
이 경로는 Selenium에서 WebDriver 인스턴스를 생성할 때 사용된다.  

<br><br> 
  
```javascript

from selenium import webdriver
from selenium.webdriver.chrome.service import Service
from webdriver_manager.chrome import ChromeDriverManager
from selenium.webdriver.common.keys import Keys
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.support.ui import WebDriverWait
from selenium.common.exceptions import ElementClickInterceptedException
from selenium.webdriver.common.by import By
import time

chrome_options = webdriver.ChromeOptions()
chrome_options.add_experimental_option("detach", True)
# `webdriver_manager`를 사용하여 ChromeDriver를 자동으로 관리하는 코드
service = Service(ChromeDriverManager().install())

SIMILAR_ACCOUNT = "cats_of_instagram"
USERNAME = "harvey_purry"
PASSWORD = ""
class InstaFollower:

    def __init__(self):
        self.driver = webdriver.Chrome(service=service, options=chrome_options)

    def login(self):
        self.driver.get("https://www.instagram.com/accounts/login/")
        time.sleep(5)

        username = self.driver.find_element(By.NAME, "username")
        password = self.driver.find_element(By.NAME, "password")

        username.send_keys(USERNAME)
        password.send_keys(PASSWORD)

        time.sleep(2)
        password.send_keys(Keys.ENTER)

    def find_followers(self):
        time.sleep(10)
        self.driver.get(f"https://www.instagram.com/{SIMILAR_ACCOUNT}")

        followers_css_selector = "a._alvs._a6hd"
        WebDriverWait(self.driver, 20).until(
            EC.element_to_be_clickable((By.CSS_SELECTOR, followers_css_selector))
        )

        followers = self.driver.find_element(By.CSS_SELECTOR, followers_css_selector)
        followers.click()

        time.sleep(2)
        modal = self.driver.find_element(By.CSS_SELECTOR, '._aano')
        self.driver.execute_script("arguments[0].scrollTop = arguments[0].scrollHeight", modal)
        time.sleep(2)
        # for i in range(10):
        #     self.driver.execute_script("arguments[0].scrollTop = arguments[0].scrollHeight", modal)
        #     time.sleep(2)

    def follow(self):
        all_buttons = self.driver.find_elements(By.CSS_SELECTOR, "button._acan")
        time.sleep(2)
        for button in all_buttons:
            try:
                button.click()
                time.sleep(1)
            except ElementClickInterceptedException:
                cancel_button = self.driver.find_element(By.XPATH, '/html/body/div[5]/div/div/div/div[3]/button[2]')
                cancel_button.click()


bot = InstaFollower()
bot.login()
bot.find_followers()
bot.follow()
```



  
