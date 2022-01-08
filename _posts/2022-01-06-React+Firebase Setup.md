---
title:  "트위터 클론코딩(1)"
excerpt: ""

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2022-01-06
last_modified_at: 2022-01-06
---
## Twitter clone-coding
트위터 클론코딩 시작🔥 <br>

<p style=font-size:12px;>
내가 참고할 강의는 노마드 코더의 트위터 클론코딩 강의이다. <br>
React를 사용하는 클론코딩 강의를 찾아보다가 이 강의에서 공부해보고싶었던 Firebase도 같이 다루길래 듣게 되었다.<br></p>

[노마드코더 강의 링크](https://nomadcoders.co/nwitter/lobby)

<p style=font-size:12px;>
나는 React를 공부중이였고, Firebase는 초면..이..다ㅎ.. 맨날 써봐야지 하다가 이제야 써본다,, <br>
이 강의에서는 HTML, CSS 그리고 React.js의 중급 정도의 지식을 요구하는 것 같다.<br>
아, 그리고 git도 함께 사용하고 있어서 git을 사용해본 사람이라면 더욱 수월하게 진행될 것 같다!!<br>
나는 강의를 들으며 수행하는 작업들을 여기해 포스팅할 생각이다. <br>
</p>

그리고 여기서 사용할 Firebase 기능에는
- Cloud Firestore : 클라우드에 호스팅 된 실시간의 비관계형(NoSQL) 데이터베이스
- Hosting : 전 세계를 대상으로 한 웹 호스팅
- Authentication : 사용자 로그인 및 ID 관리
- Cloud Storages : 거대하게 확장할 수 있는 파일 스토리지

이렇게 4가지 기능을 사용한다고 한다!!<br>
그럼 본격적으로 시작해보겠다!!

## React + Firebase Setup

### React application 생성

터미널이나 cmd 창에서 프로젝트를 생성할 폴더로 이동한 후 아래 명령어를 실행해준다.

~~~
npx creat-react-app [프로젝트 명]
~~~

나는 프로젝트 명을 twitter_clone-coding 으로 해주었다.

![image](https://user-images.githubusercontent.com/91127380/148337582-484a9736-da5f-4ea3-b2fb-3555320a23fc.png)

대충 이런 결과가 나왔디면 React 프로젝트 생성에 성공!

