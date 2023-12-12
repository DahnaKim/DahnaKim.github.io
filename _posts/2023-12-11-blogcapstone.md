---
layout: post
title: Python Day67
subtitle: Blog Capstone Project - RESTful Routing
cover-img: /assets/img/20231211_67_13.png
thumbnail-img: /assets/img/20231211_67_13.png
share-img: /assets/img/20231211_67_13.png
tags: [Day67, clang, blog capstone, RESTful, SQLite, CKEditor, jinja filter, safe, striptag, flask, is_edit]
---
       
<br><br>
  
# Blog Capstone Project - RESTful Routing  

<br>

**Clang** : C, C++, Objective-C, 그리고 Objective-C++ 프로그래밍 언어를 위한 컴파일러  
LLVM 프로젝트의 일부로, GCC 컴파일러 스위트에 대한 고성능, 오픈 소스, 모듈식 대안을 제공한다. 특히 빠른 컴파일 시간, 우수한 메모리 관리, 그리고 사용자에게 명확한 오류 메시지를 제공함.  
**파이썬 프로젝트에서 Clang을 요구하는 이유** ⇨ 예를 들어, 프로젝트가 C나 C++로 작성된 확장 모듈을 포함하고 있거나,   
특정 C/C++ 라이브러리에 의존하는 경우 Clang 컴파일러가 필요할 수 있음. 또한, 프로젝트가 특정 플랫폼 또는 환경에서 최적화된 성능을 제공하기 위해 Clang의 특정 기능을 활용할 수 있다.  

<br>

- `app.run(debug=True)` : 	Flask 애플리케이션을 기본 호스트(127.0.0.1 또는 localhost)와 기본 포트(5000)에서 실행  
debug=True 옵션은 디버그 모드를 활성화  
이 모드에서는 코드 변경 사항이 자동으로 적용되고, 오류 발생 시 상세한 디버그 정보가 브라우저에 표시됨  
개발 중에 로컬 컴퓨터에서 애플리케이션을 테스트할 때 주로 사용  

<br>

- `app.run(host='0.0.0.0', port=5000)` : Flask 애플리케이션을 모든 공용 IP 주소에서 접근 가능하게 만듦.  
즉, 로컬 네트워크 내의 다른 컴퓨터나 장치에서도 애플리케이션에 접근할 수 있다. 개발 중이지만 애플리케이션을 로컬 네트워크상의 다른 사용자와 공유하고자 할 때 사용할 수 있음  

<br>

**CKEditor**  
  
![1](/assets/img/20231208_67_1.png)  

<br><br>
  
## 블로그 게시물 항목을 가져오기  
  
```javascript
@app.route('/')
def get_all_posts():
    posts = BlogPost.query.all()
    return render_template("index.html", all_posts=posts)
```

<br>

![10](/assets/img/20231211_67_10.png)

<br><br>

## 신규 블로그 게시물을 게시  

<br>
  
**index.html**  
  
![3](/assets/img/20231208_67_3.png)  

<br>
  
**main.py**  
  
![4](/assets/img/20231208_67_4.png)  

<br>
  
**make-post.html**  
  
![5](/assets/img/20231208_67_5.png)  

<br>

![6](/assets/img/20231208_67_6.png)  

<br>

![2](/assets/img/20231208_67_2.png)  

<br>

- 날짜는 서버의 datetime 모듈을 사용하여 자동으로 계산되어야 함  
  
`from datetime import date` 추가  

<br>
  
- 모든 필드 입력 후 데이터를 post.db에 BlogPost객체로 저장

<br>

- 저장 후 홈페이지로 리디렉션, 새 게시물 표시

<br>

![7](/assets/img/20231211_67_7.png)  

<br>

![8](/assets/img/20231211_67_8.png)  

<br>

![9](/assets/img/20231211_67_9.png)  

<br>

![11](/assets/img/20231211_67_11.png)  

<br><br>

## 기존 블로그 게시물을 편집  
  
![12](/assets/img/20231211_67_12.png)

<br>

![13](/assets/img/20231211_67_13.png)

<br>

![14](/assets/img/20231211_67_14.png)

<br><br>

## 블로그 게시물을 삭제  
  
![15](/assets/img/20231211_67_15.png)

<br>

![16](/assets/img/20231211_67_16.png)

<br>

![17](/assets/img/20231211_67_16.png)  

<br>
  
**파일경로** : /Users/dana/Downloads/day-67-RESTful-blog-start   

<br><br>





