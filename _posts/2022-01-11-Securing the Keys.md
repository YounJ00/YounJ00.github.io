---
title:  "트위터 클론코딩(2)"
excerpt: ""

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2022-01-11
last_modified_at: 2022-01-11
---
## Securing the Keys
우리는 전 포스팅에서 firebase.js(firebaseConfig)에 보안key들을 설정해놓았다.
![image](https://user-images.githubusercontent.com/91127380/148732955-b19f92dd-dd5c-40ce-a2fb-6a7d736c05ba.png)

하지만 이 코드를 그대로 git이나 다른 곳에 공유할 경우에 보안 문제가 생길 수 있다.<br>
그래서 우리는 따로 .env 라는 파일을 만들어서 보안 문제를 해결하려고 한다.

### Step 1 : .env 파일 생성
![image](https://user-images.githubusercontent.com/91127380/148873021-79cc3a21-67bb-45fd-867c-dc581cb9f9c2.png)

.env 파일을 생성 한 후 [REACT_APP_SOMETHING] 이런 식으로 앞에 REACRT_APP으로 시작 해 뒤에 이름을 붙여 환경변수를 만들어준다.
- REACT_APP_API_KEY
- REACT_APP_AUTH_DOMAIN
- REACT_APP_PROJECT_ID
- REACT_APP_STORAGE_BUCKET
- REACT_APP_MESSAGIN_ID
- REACT_APP_APP_ID

### Step 2 : firebase.js 파일 수정
그런다음 firebase.js 파일을 아래와 같이 변경해준다. 

~~~
const firebaseConfig = {
    apiKey: process.env.REACT_APP_API_KEY,
    authDomain: process.env.REACT_APP_AUTH_DOMAIN,
    projectId: process.env.REACT_APP_PROJECT_ID,
    storageBucket: process.env.REACT_APP_STORAGE_BUCKET,
    messagingSenderId: process.env.REACT_APP_MESSAGIN_ID,
    appId: process.env.REACT_APP_APP_ID
  };
~~~

![image](https://user-images.githubusercontent.com/91127380/148898717-1634f61b-ca7f-4795-b6fc-87ac05c71756.png)

### Step 3 : .gitignore 파일 수정
여기서 .gitignore 파일에 .env를 추가해주면 실제 직접적인 나의 key값들은 보이지 않고, firebase.js 파일의 환경변수들만 보이게 된다.<br>
![image](https://user-images.githubusercontent.com/91127380/148901198-b1b1157d-7646-4028-adcd-43b087eec4f0.png)

하지만 이것만 가지고 나의 key값 들이 노출되는 걸 완전히 막을 수 있는 것은 아니다.<br>
왜냐하면 내가 Firebase를 사용하고자 한다면 client로부터 요청을 받아야 하고, 코드를 빌드하고 받아서 전환하는 과정에서 변수들을 실제 값들로 바꾸게 되게 때문이다. <br>
그런데도 이렇게 해주는 이유는 오직 Github에 나의 코드를 업로드할 때 실제 key값들은 보이지않게 하기 위해서이다.
<br><br>
다음 포스팅에서는 Router Setup 과정에 대해 공부해 볼 것이다!!