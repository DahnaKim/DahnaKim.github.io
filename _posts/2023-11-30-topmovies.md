---
layout: post
title: Python Day64
subtitle: My Top 10 Movies Project(1)
cover-img: /assets/img/20231130_64_9.png
thumbnail-img: /assets/img/20231130_64_9.png
share-img: /assets/img/20231130_64_9.png
tags: [Day64, movies project, api, flask, sqlite, SQLAlchemy, WTForms, bootstrap, database, CRUD]
---
       
<br><br>

# My Top 10 Movies Project(1)  
  
![1](/assets/img/20231130_64_1.png)  
<br>

`app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///movies.db'` : Flask 애플리케이션의 구성을 설정  
`SQLALCHEMY_DATABASE_URI`는 SQLAlchemy가 사용할 데이터베이스의 위치와 종류를 지정하는 설정 키임  
`sqlite:///movies.db`는 SQLite 데이터베이스를 사용하고, 이 데이터베이스 파일은 movies.db라는 이름으로 현재 파일이 있는 같은 디렉토리에 저장   
  
![3](/assets/img/20231130_64_3.png)  
<br>
![2](/assets/img/20231130_64_2.png)  
<br>
![4](/assets/img/20231130_64_4.png)  
<br>
![5](/assets/img/20231130_64_5.png)  
<br>
![6](/assets/img/20231130_64_6.png)  
<br>
![7](/assets/img/20231130_64_7.png)  
<br>
![8](/assets/img/20231130_64_8.png)  
<br>

`all_movies = Movie.query.order_by(Movie.rating).all()` : 데이터베이스에서 모든 영화 데이터를 조회   
  
Movie.query.order_by(Movie.rating) - Movie 테이블에서 모든 레코드를 rating 필드의 값에 따라 정렬   
  
![9](/assets/img/20231130_64_9.png)  

<br>
