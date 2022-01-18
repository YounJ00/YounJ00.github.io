---
title:  "트위터 클론코딩(4) - Using Firebase Auth"
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
- import부분에 useState를 추가해준다.

이제 Router은 prop(isLoggedIn)을 전달 받았고