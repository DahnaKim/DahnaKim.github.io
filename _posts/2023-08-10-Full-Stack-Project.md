---
layout: post
title: 0810 프로젝트 수정작업
subtitle: ItemDetail 안의 댓글창 클릭이 안되는 문제
tags: [fullstack,project,fix]
comments: true
---

잠결에 팀원들 대화를 보니 댓글 기능이 클릭조차 되지 않아  
내가 두번째로 삽질 오래한 페이지를 갈아 엎을 계획을 세우고 있었다ㅠㅠ  
어케든 살려보려고 별의별짓을 다 해봤는데 결국 살림!ㅠㅠㅠ  
후후후후후훟흐흐흐🤤

## 변경파일

ItemListPaging.js  
node_modules   
ReplyList.js  
ReplyInsert.js  
ItemDetail.js  
ItemDetail.module.css  


**fixed**  
 - 아이템리스트에서 페이지 화살표가 사라진 문제  
   💡 모듈에 패키지 인스톨 후 ItemListPaging.js에 fortawesome import시킴

- 아이템디테일 구매, 수정 버튼 호버시 파란 링크로 뜨는 폰트색상 변경
  
- 댓글 클릭이 안되는 문제 수정  
ReplyList.js, ReplyInsert.js 기존 스타일 제거하고 컨테이너 분류도 해봤으나 안됨..  
z-index 여기저기 다 입혀봐도 안돼서 이것저것 한줄씩 지워보다가 
styles.box를 지워버리니까 클릭이 됨..ㅋ

**💡원인은  .box:before의 position: absolute 때문  
.box:before가 .box 위에 위치하여 그 안의 내용들이 클릭되지 못하게 하는 역할을 함**

{: .box-note}
**Note:** ItemDetail.module.css에서
.box에 z-index: 1;
.box:before에는 z-index: -1; 로 box보다 낮게 설정  
마지막으로 ItemDetail.js의 댓글관련 불러오는 코드에도 zIndex: 2를 넣어줘서 상위에 올림

- 댓글 인풋박스 하단으로 이동, 작성 버튼은 살짝 위로 이동해서 라인 맞춤   
  
<div style="text-align: center;">
<video width="640" height="480" controls>
  <source src="/assets/img/replyInsert.mp4" type="video/mp4">
</video>


