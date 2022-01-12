---
title:  "트위터 클론코딩(3)"
excerpt: ""

categories:
  - Blog
tags:
  - [Blog, jekyll, Github, Git]

toc: true
toc_sticky: true
 
date: 2022-01-12
last_modified_at: 2022-01-12
---
## Router Setup
우리는 이제 우리의 application의 구조를 잡아햐 한다.<br>

### Step 1 : Components Routers 폴더 생성

![image](https://user-images.githubusercontent.com/91127380/149077029-3544c288-3e41-400a-a168-39064b88d01d.png)

![image](https://user-images.githubusercontent.com/91127380/149077326-11a3fa5c-8ea7-422e-903c-1de1ecf6a57e.png) ![image](https://user-images.githubusercontent.com/91127380/149077643-4c1c6815-0850-4e89-8b25-8610222c5bf1.png)

- App.js 파일을 components 폴더로 이동시켜준다.
- index.js 파일에서 App.js의 import 경로를 수정해준다. (./App -> ./components/App)

![image](https://user-images.githubusercontent.com/91127380/149078241-528cfeb2-f1a3-4037-b441-e256cdc5021f.png)


### Step 2 : Route 생성
- 우리는 이제 routes폴더에 기본적으로 우리가 설정할 route들을 생성해야 한다.
- 아마 4개 정도의 route를 만들 예정이다.<br>
- 로그인 되어있지 않다면 로그인을 위한 부분을 보여주고, 로그인이 된 이후에는 Home으로 이동하게 될 거다. (Authentication)<br>
- Home에서는 기본적으로 트윗을 작성할 수 있고, 업로드 되는 트윗들을 볼 수 있다. (Home)<br>
- 그리고 나의 프로필로도 이동해서 또 프로필을 수정할 수 있는 설정으로 들어갈 수 있게 될 거다. (Profile, EditProfile)

#### 1. Authentication
- routes폴더 안에 Auth.js파일을 생성해준다.
![image](https://user-images.githubusercontent.com/91127380/149080222-55f13efd-642f-4587-92cc-cfb675f336a6.png)


#### 2. Home
- routes폴더 안에 Home.js파일을 생성해준다.
![image](https://user-images.githubusercontent.com/91127380/149080599-4e9f5f0d-8191-44dd-9441-932da5680e0c.png)


#### 3. Profile
- routes폴더 안에 Profile.js파일을 생성해준다.
![image](https://user-images.githubusercontent.com/91127380/149080994-61f76521-4bc1-42da-a80f-9e531adfc0bb.png)


#### 4. EditProfile
- routes폴더 안에 EditProfile.js파일을 생성해준다.
![image](https://user-images.githubusercontent.com/91127380/149081414-4772394a-1ed1-4efd-9470-7709037e1a9d.png)

### Step 3 : Router 만들기
#### react-router-dom 설치
최근에 react-router-dom이 v6으로 업데이트 되면서 최신버전으로 설치한다면 많은 오류가 생길 것 같아서, 나는 npm i react-router-dom@5.2.0으로 다운그레이드해주었다. <br>
좀 더 쉽게 따라 하고 싶다면 밑의 버전을 다운받는 것을 추천한다.

VsCode 터미널에서 아래 명령어를 실행해준다.
~~~
npm i react-router-dom@5.2.0
~~~

#### Router.js 파일 생성
components폴더에 Router를 만들어 줄 것이기 때문에, Router.js파일을 생성해준다.

- 이제부터 우리가 render시킬 routes는 우리의 로그인 여부에 따라 달라질 거다.

![image](https://user-images.githubusercontent.com/91127380/149092257-495cee01-829d-4068-b778-75e5f55c89f3.png)

~~~
const [isLoggedIn, setIsLoggedIn] = useState(false);
~~~
//Hook 설명(useState)

~~~
<Switch>
                {isLoggedIn ? (
                    <>
                        <Route exact path="/">
                            <Home />
                        </Route>
                    </> 
                ) : ( 
                    <Route exact path="/">
                        <Auth /> 
                    </Route> 
                )}
            </Switch>
~~~
//Switch부분 설명

~~~
import Auth from "../routes/Auth";
import Home from "../routes/Home";
~~~
//사용하는 파일 import 해주는거 설명

### App.js 수정
앞에서 만든 AppRouter를 render해준다.
![image](https://user-images.githubusercontent.com/91127380/149092380-76fcaab4-3aa0-4cdf-9427-5c6be2a38ba0.png)

