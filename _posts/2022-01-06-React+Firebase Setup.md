---
title:  "트위터 클론코딩(1) - React+Firebase Setup"
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

그리고 여기서 사용할 Firebase 기능에는
- Cloud Firestore : 클라우드에 호스팅 된 실시간의 비관계형(NoSQL) 데이터베이스
- Hosting : 전 세계를 대상으로 한 웹 호스팅
- Authentication : 사용자 로그인 및 ID 관리
- Cloud Storages : 거대하게 확장할 수 있는 파일 스토리지

이렇게 4가지 기능을 사용한다고 한다!!<br>
그럼 본격적으로 시작해보겠다!!

## React + Firebase Setup

### Step 1 : React application 생성

터미널이나 cmd 창에서 프로젝트를 생성할 폴더로 이동한 후 아래 명령어를 실행해준다.

~~~
npx creat-react-app [프로젝트 명]
~~~

나는 프로젝트 명을 twitter_clone-coding 으로 해주었다.

![image](https://user-images.githubusercontent.com/91127380/148337582-484a9736-da5f-4ea3-b2fb-3555320a23fc.png)

대충 이런 결과가 나왔디면 React 프로젝트 생성에 성공!

### Step 2 : Git Repository 생성 및 연결
그 다음 레파지토리를 만들어 주소를 복사해준다.
![image](https://user-images.githubusercontent.com/91127380/148723703-5c23f1d2-1eee-4472-9802-6f6d030a88d2.png)

VsCode에서 React 프로젝트를 열어준다음 Terminal 창에서 앞에서 생성한 git 레파지토리와 연결해준다.
~~~
git init
git remote add origin [생성한 레파지토리 URL]
~~~

![image](https://user-images.githubusercontent.com/91127380/148723854-a6833d6b-1e8f-45f2-85f8-dd9e49f15cc2.png)

### Step 3 : create-react-app 파일 정리
이제 우리는 create-react-app 으로 생성한 React 프로젝트 파일을 정리해 줄 것이다. create-react-app 은 생각보다 많은 파일들을 생성해내기 때문에 우리가 사용하지 않을 파일들을 지워줄 것이다.

우선, [index.js] 파일에서 css 부분을 지워준다.
![image](https://user-images.githubusercontent.com/91127380/148724794-5322f629-9543-437f-90bb-89daa97087d7.png)

[App.js]는 css와 svg를 지워준 후 이 상태가 우리의 App.js 모습이어야 한다.
![image](https://user-images.githubusercontent.com/91127380/148725351-f51bb6a2-fe77-40d7-95a0-18ca07e69af3.png)

필요없는 파일들을 지워준다.
- App.css
- App.test.js
- index.css
- logo.svg
- reportWebVitals.js
- setupTests.js

![image](https://user-images.githubusercontent.com/91127380/148726182-111b8220-9c5b-4e03-b3cc-d87465bfec96.png)

우리는 test를 해보지 않을것이기 때문에 [package.json]에서 test 부분도 지워준다.
![image](https://user-images.githubusercontent.com/91127380/148726315-e84b2c63-5402-4520-af49-f34bd33f67ed.png)

그러면 정리 끝!! 파일들이 전보다 훨씬 깔끔하게 정리 된 것을 확인할 수 있다.

VsCode Terminal에서 아래 명령어를 입력해 레파지토리에 파일을 업로드해준다.
~~~
git add .
git commit -m "커밋 메시지"
git push origin master
~~~
나는 커밋 메시지를 React.js setting 으로 해주었다. 같은 메시지로 커밋 할 필요는 없다!!

![image](https://user-images.githubusercontent.com/91127380/148726972-76a44f8c-38f1-4008-8080-fbd993410d03.png)

### Step 4 : Firebase 프로젝트 생성
![image](https://user-images.githubusercontent.com/91127380/148727534-aa7d417e-5330-4fb3-bca6-b4858dc6ed3a.png)
Firebase 사이트에서 프로젝트를 생성해준다.

![image](https://user-images.githubusercontent.com/91127380/148727646-54af656f-9fad-43c4-b5ae-a785f33548fe.png)

![image](https://user-images.githubusercontent.com/91127380/148727710-d347a04a-6246-4341-a90d-436683a5f133.png)

![image](https://user-images.githubusercontent.com/91127380/148727851-cb45f58a-4cba-4dce-bdf7-0c14b50f47fc.png)
프로젝트 생성 성공!!!

![image](https://user-images.githubusercontent.com/91127380/148729892-21e79149-9d9c-461d-9506-2c5964e57ec4.png)

### Step 5 : Firebase SDK 설치
이제 우리는 firebase SDK를 설치해줘야한다.
우리는 React 식의 방법을 사용할 것이다. 
[JavaScript SDK](https://firebase.google.com/docs/web/setup?authuser=0) 에 들어가보면 SDK를 설치하는 다양한 방법들을 볼 수 있다. 링크를 복사해서 추가해주는 방법도 있고, npm 명령어를 통해 추가해주는 방법이 있다.<br>
우리는 아래 명령어를 실행하여 추가해 줄 것이다.
~~~
npm install --save firebase@9.6.1
~~~

그 다음 firebase.js 파일을 추가해주고 아래 코드를 넣어준다.
~~~javascript
import firebase from "firebase/compat/app";
import "firebase/compat/auth";
import "firebase/compat/firestore";
import "firebase/compat/storage";

const firebaseConfig = {
    apiKey: "AIzaSyBmdjDPDzUVCZG6cl-QoA05PDbk3r7ecEU",
    authDomain: "twitter-7190e.firebaseapp.com",
    projectId: "twitter-7190e",
    storageBucket: "twitter-7190e.appspot.com",
    messagingSenderId: "346370097254",
    appId: "1:346370097254:web:babdb8b799f0446e80ada7"
  };

  export default firebase.initializeApp(firebaseConfig);
~~~
firebaseConfig 부분은 각자 생성된 코드를 넣어주면 된다.
![image](https://user-images.githubusercontent.com/91127380/148870258-a87b6d57-1ff6-4f48-a404-8cc8b44d2dea.png)

![image](https://user-images.githubusercontent.com/91127380/148732955-b19f92dd-dd5c-40ce-a2fb-6a7d736c05ba.png)

이제 VsCode Terminal에 npm run start 또는 yarn start 명령으로 서버를 실행시켜보자!

![image](https://user-images.githubusercontent.com/91127380/148735527-f59ed20c-af0e-4b6f-979f-bbfa3493b601.png)

이제 React.js 셋업할 준비가 완료된거다.

다음 포스팅에서는 firebase.js 파일에 추가해준 각자 고유의 key를 보안하는 방법에 대해 알아볼 것이다!!
