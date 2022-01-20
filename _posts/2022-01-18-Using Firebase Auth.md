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
### Step 1 : Router 파일 정리
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

### Step 2 : Auth import
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

### Step 3 : Auth 호출
우선 아래 코드를 App.js파일에 추가 작성해준다.
~~~javascript
const auth = fbase.auth();
~~~
![image](https://user-images.githubusercontent.com/91127380/150051560-1f20a457-a3bc-4274-9756-ed9df893bd52.png)

하지만 우리는 앞으로 auth 서비스를 아주 많이 호출할 예정이다.<br>
그래서 더 편하게 코드를 수정해 줄 것이다.<br><br>
firebase.js 파일을 아래처럼 수정해준다.

![image](https://user-images.githubusercontent.com/91127380/150273276-e168a092-e2af-4374-a4b2-766749593115.png)
~~~javascript
export const authService = firebase.auth();
~~~
authService라는 firebase.auth()객체를 만들어준다.

우리는 이제 App.js 에서 유저를 가져와서 로그인 여부를 판단하도록 해줄 것이다.<br>

![image](https://user-images.githubusercontent.com/91127380/150275062-3088ce2e-a9c7-4a9c-945d-228cb8cf18f7.png)
- fbase import부분에 authService를 받아온다.
~~~javascript
console.log(authService.currentUser);
~~~
- 우리가 받아온 authService를 통해 현재 유저의 상태를 가져온다.
- 현재 유저의 상태인 authService.currentUser를 콘솔에 출력해준다.
- 콘솔에는 현재 User 아니면 null 값이 반환될 것이다.

현재 로그인되지 않은 상태이기 때문에 다시 서버를 실행시켜보면 콘솔창에 null값이 출력된 것을 확인할 수있다.
![image](https://user-images.githubusercontent.com/91127380/150275127-80877f3b-f33a-4fce-841c-b982b87e569d.png)

이제 우리는 useState의 기본 값을 <b>authService.currentUser</b> 값으로 바꿔 줌으로써 useState는 유저의 로그인 여부를 알 수 있게 된다.
~~~javascript
const [isLoggedIn, setIsLoggedIn] = useState(authService.currentUser);
~~~
결과적으로 서버를 실행시켜보면 유저가 로그인되기 전 화면인 Auth 가 나타나게 된다.
![image](https://user-images.githubusercontent.com/91127380/150277036-bd7073e3-9708-482d-8dc8-a9ae24697c51.png)

여기까지 우리는 로그인 여부를 판별핧 수 있게 되었다!! 다음으로는 Login Form을 만들어 볼 거다.!

## Login Form part One
### Step 1 : Firebase Authentication 추가 설정
먼저 firebase 콘솔에서 Authentication 섹션으로 이동하면 현재 아무 유저도 없다는 걸 볼 수 있다.<br>
![image](https://user-images.githubusercontent.com/91127380/150290438-112678c9-f762-4d68-bcbd-448039bb7603.png)

여기서 <b>'로그인 방법 설정'</b> 버튼을 눌러준다.<br>
우리가 가진 선택지들 중에 <b>'이메일/비밀번호'</b>와 <b>'구글'</b>을 선택한 후 저장해준다.
![image](https://user-images.githubusercontent.com/91127380/150291966-09ccd4fe-f7ef-4b9f-93ee-575ff2321f9f.png)
![image](https://user-images.githubusercontent.com/91127380/150292309-2f8ab5e7-adb6-4a2e-8361-ac53c6aa5d5b.png)

그리고 <b>'Github'</b>도 사용가능하다.<br>
![image](https://user-images.githubusercontent.com/91127380/150293793-3e76530b-7dc1-4c40-919c-f0a7456d8db2.png)
- Github를 사용하려면 먼저 Github에서 app을 설정해야한다.<br>
- Github > Settings > Developer settings 으로 이동해준다.<br>
- 그다음 OAuth Apps에서 'Register a new application'버튼을 클릭해 새로운 app을 생성해준다.

![image](https://user-images.githubusercontent.com/91127380/150293231-03eaba64-7f41-4f0e-994a-6c533e04c7dd.png)
'Homepage URL'과 'Authorization callback URL'에는 위에 Firebase 설정페이지 밑에 게시 된 URL을 복사해와 붙여준다.
![image](https://user-images.githubusercontent.com/91127380/150295129-485cc4e5-a5b2-4d3a-83c5-d258876cfebb.png)
![image](https://user-images.githubusercontent.com/91127380/150294261-0e8074ff-1f04-4188-81fb-b87b0fc1a196.png)

다 입력했다면 'Register application' 버튼을 눌러 app을 만들어준다.<br>
그러면 <b>'Client ID'</b>와 <b>'Client Secret'</b>이 발급될 텐데,<br> 
이것을 사용해서 Firebase Authentication Github설정에 입력해준다.
![image](https://user-images.githubusercontent.com/91127380/150296049-03b3ad07-9635-49ac-a639-674726fb2d8a.png)
![image](https://user-images.githubusercontent.com/91127380/150296504-f7601f62-c7aa-4268-a61c-e9b20848ec3a.png)

이렇게해서 Firebase Authentication 설정이 끝났다!!<br>
이제 우리는 Login Form 페이지를 한 번 만들어 볼 거다.

### Step 2 : Login Form Page (Auth.js)
일단 Auth.js의 수정된 코드 먼저 보여주고 설명을 하겠다.
~~~javascript
import React, { useState } from "react";

const Auth = () => {
    const [email, setEmail] = useState("");
    const [password, setPassword] = useState("");
    const onChange = (event) => {
        const {
            target : {name, value}
        } = event;
        if (name === "email") {
            setEmail(value);
        } else if (name === "password") {
            setPassword(value);
        }
    };
    const onSubmit = (event) => {
        event.preventDefault();
    };
    return (
        <div>
            <form onSubmit={onSubmit}>
                <input
                    name="email"
                    type="text"
                    placeholder="Email"
                    required
                    value={email}
                    onChange={onChange}
                />
                <input
                    name="password"
                    type="password"
                    placeholder="Password"
                    required
                    value={password}
                    onChange={onChange}
                />
                <input type="submit" value="Log In" />
            </form>
            <div>
                <button>Continue with Google</button>
                <button>Continue with Github</button>
            </div>
        </div>
    )
}
export default Auth;
~~~
