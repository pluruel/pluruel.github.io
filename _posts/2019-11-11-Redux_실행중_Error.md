---
layout: post
title:  "Redux 구현중 Error"
date:   2019-11-11 13:50:10 +0900
categories: #react #redux #js
---

# Redux-Thunk 사용 중 다음과 같은 에러 문구

~~~
“Actions must be plain objects. Use custom middleware for async actions.” 
~~~

## 해결 방법
---
### 미들웨어가 등록이 되지 않았을 수 있다.

스토어를 생성하며, 미들웨어를 등록해주자!
~~~js
const store = createStore(rootReducer, applyMiddleware(logger, ReduxThunk));
// index.js
~~~

### 이름이 잘못되어 있을 수 있다.

이렇게 에러가 발생되면 아주 난감해지는데, 기본적으로 주의해야 할 것들이있다.
const혹은 let의 변수 선언에 기존에 이미 작성되어있는 ex) props 등등 을 사용하게되면 정말로 이해할 수 없는 에러들이 반복적으로 나타나게된다. 때로는 위의 에러가 뜨지만 때로는 

~~~
Uncaught TypeError: Cannot read property 'type' of undefined
~~~
이런 류의 에러가 발생하게 되는데, 진짜 난감해진다.

원천적으로 자동완성에 나타나는 이름들은 가능하면 변수로 사용하지 말자.   
(이유가 확실하지는 않으나 경험적으로 생겼던 문제. 완전한 분석은 하지 않음.)