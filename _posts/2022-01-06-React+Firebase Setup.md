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

내가 참고할 강의는 노마드 코더의 트위터 클론코딩 강의이다. <br>
React를 사용하는 클론코딩 강의를 찾아보다가 이 강의에서 공부해보고싶었던 Firebase도 같이 다루길래 듣게 되었다.<br>
[노마드코더 강의 링크](https://nomadcoders.co/nwitter/lobby)

나는 React를 공부중이였고, Firebase는 초면..이..다ㅎ.. 맨날 써봐야지 하다가 이제야 써본다,, <br>
이 강의에서는 HTML, CSS 그리고 React.js의 중급 정도의 지식을 요구하는 것 같다.<br>
아, 그리고 git도 함께 사용하고 있어서 git을 사용해본 사람이라면 더욱 수월하게 진행될 것 같다!!<br>
나는 강의를 들으며 수행하는 작업들을 여기해 포스팅할 생각이다. <br>
 끝까지 할 수 있을 지는 모르겠지만,, 목표는 강의를 듣지 않아도 이 블로그 글 만으로도 쉽게 따라 할 수 있을 정도로 자세하게 정리해 볼 생각이다!!🔥

그리고 여기서 사용할 Firebase 기능에는
- Cloud Firestore
- Hosting
- Authentication
- Cloud Storages

이렇게 4가지 기능을 사용한다고 한다!!<br>
그럼 본격적으로 시작해보겠다!!

### 먼저 React 프로젝트를 생성해준다.

터미널이나 cmd 창에서 아래 명령어를 실행해준다.

~~~
npx creat-react-app [프로젝트 명]
~~~

나는 프로젝트 명을 twitter_clone-coding 으로 해주었다.

![image](https://user-images.githubusercontent.com/91127380/148337582-484a9736-da5f-4ea3-b2fb-3555320a23fc.png)

