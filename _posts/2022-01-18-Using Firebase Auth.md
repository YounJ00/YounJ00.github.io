---
title:  "트위터 클론코딩(4) - Authentication"
excerpt: ""

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2022-01-18
last_modified_at: 2022-01-18
---
## Using Firebase Auth
### Router 파일 정리
우리는 먼저 Router파일 정리를 해 줄 것이다.<br>
Router.js 파일은 Routes들만 보여줄 수 있도록 정리한다.

![image](https://user-images.githubusercontent.com/91127380/149885234-596a80d0-7d18-45d6-8279-aa8a87fe296c.png)
~~~javascript
const [isLoggedIn, setIsLoggedIn] = useState(false);
~~~
- Router.js 에 있던 useState()부분을 App.js파일에 넣어준다.

~~~javascript
return <AppRouter isLoggedIn={isLoggedIn} />;
~~~
- 그 다음에는 isLoggedIn을 prop으로 Router에 넘겨준다.

~~~javascript
import React, { useState } from 'react';
~~~
- import부분에 useState를 추가로 정의해준다.

![image](https://user-images.githubusercontent.com/91127380/149885717-5f58a59e-fe21-41ca-89d7-c9777d50941b.png)

이제 Router은 prop(isLoggedIn)을 전달 받았고, AppRouter에서 파라미터값으로 받아준다.

우리는 앞으로 App.js 에서 모든 로직들을 다룰 것이다.<br>
App() 안에 AppRouter를 사용하는 이유는 AppRouter 외에도 분리된 로직들을 쓸 수 있게하기 위해서이다.<br>
예를들어 <footer></footer>를 추가해보자. 아래 코드를 AppRouter 밑에 추가해주자.
~~~javascript
<footer> &copy; {new Date().getFullYear()} Twitter </footer>
~~~
![image](https://user-images.githubusercontent.com/91127380/149889734-64e469fd-46d3-4f91-8731-f5e316f256ad.png)
그러면 AppRouter부분 밑에 위에서 추가해주었던 footer가 나타난 것을 확인할 수 있다.

### Auth import
이제부터는 Authentication을 다뤄보자.
우리가 auth를 사용하고자 한다면 제일 먼저 이것을 import 해줘야 한다.<br>
firebase.js 파일에 우리가 사용할 auth, firestore, storage 등을 import해준다.
![image](https://user-images.githubusercontent.com/91127380/149893333-5bd47e77-67de-4d81-ba14-2d50c338db8e.png)

이제 이 firebase.js 파일을 App.js파일에 import 해줘야한다.
~~~javascript
import firebase from '../firebase';
~~~
파일앞에 ../는 파일의 경로를 나타낸다.

여기서 우리는 파일경로를 하나하나 표시해주는 방법 대신에 Absolute import 를 사용해 줄 것이다.<br>
jsconfig.json 파일을 생성한 후 아래 코드를 작성해준다.
~~~javascript
{
    "compilerOptions": {
        "baseUrl": "src"
    },
    "include": ["src"]
}
~~~
![image](https://user-images.githubusercontent.com/91127380/149896710-90c13d73-56e8-4e36-b924-74813e2bcce3.png)

우리는 지금까지 무언가를 import해줄 때 파일 앞에 파일 경로를 표시해주었다.<br>
하지만 Absolute import방법을 사용하여 파일 경로 대신에 [폴더명/파일명]로 해줄 수 있다.

그 전에 firebase.js 파일명을 바꿔줄 거다.<br>
기존의 firebase 명령과 헷갈리기 쉽기 때문에 firebase.js 대신에 fbase.js로 바꿔준다.

~~~javascript
import AppRouter from 'components/Router';
import fbase from 'fbase';
~~~
그러면 이제 [폴더명/파일명]으로 import가 가능하다.<br>
여기서 npm start를 통해 서버가 잘 돌아가는지 한 번 확인해주자!! 오류 없이 잘 돌아간다면 다음으로🔥

### Auth 호출
우선 아래 코드를 App.js파일에 추가 작성해준다.
~~~javascript
const auth = fbase.auth();
~~~
![image](https://user-images.githubusercontent.com/91127380/150051560-1f20a457-a3bc-4274-9756-ed9df893bd52.png)

하지만 우리는 앞으로 auth 서비스를 아주 많이 호출할 예정이다.<br>
그래서 더 편하게 코드를 수정해 줄 것이다.<br><br>
firebase.js 파일을 아래처럼 수정해준다.

![image](https://user-images.githubusercontent.com/91127380/150052309-9ebf6e6e-3208-4ab8-928c-4b15570ba3e9.png)
~~~javascript
export const authService = firebase.auth();
~~~
authService라는 firebase.auth()객체를 만들어준다.

## Login Form part One