---
layout: post
title:  "Redux"
date:   2019-09-04 14:50:10 +0900
categories: #node
---

# Koa

Express 개발자들이 부족한 부분을 추가한 미들웨어

자체 기능은 Express보다 적으나, 다양한 모듈을 사용하여 입맛대로 개발이 가능하다.

## use() 
Koa의 미들웨어 함수
여기서 사용 된 ctx는 다양한 기능을 담고 있는데,
.status를 통해 미리 지정된 401 에러라던가
.query명령어로 url우측에 /?authorized=1 등으로 넘겨줄 수 있다.(parameter 개념)

## next()

메소드를 선언한 순서로 미들웨어를 돌린다.
next()를 call 하면 다음(코드의 밑)에 선언한 use가 불린다.


~~~js
app.use((ctx, next) => {
    if(ctx.query.authorized !== '1') {
        ctx.status = 401;
        return;
    }
    console.log(ctx.url);
    console.log(1);
    next().then(() => {
        console.log('END')
    })
})


app.use((ctx, next) => {
    console.log(2);
    next()
})
~~~

# router

~~~js
router.get('/', ctx=> {
    ctx.body= 'home'
})

router.get('/about', ctx=>{
    ctx.body = '소개'
})
// ${}를 쓰기 위해서는 '가 아닌 `를 씀에 주의할 것 
router.get('/about/:name?', ctx=>{
    const { name } = ctx.params;
    ctx.body = name? `${name} 소개` : '소개'
})

router.get('/posts', ctx=>{
    const { id } = ctx.query;
    ctx.body = id? `포스트 # ${id}`: '포스트 아이디가 없음.'
})


app.use(router.routes()).use(router.allowedMethods())
~~~
코드를 분석해 보면 app.use 를 간결하게 줄였다고 볼 수 있겠다

# REST

~~~js

~~~
