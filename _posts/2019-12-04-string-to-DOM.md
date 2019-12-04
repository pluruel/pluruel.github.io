---
layout: post
title: "String2DOM"
date: 2019-12-04 09:50:10 +0900
categories: #react #redux #js
---

# Issue

JSON으로 관리되는 객체를 특정 Lib등을 통해 DOM의 형태로 문자열 화 시킨경우, DOM자체는 신뢰할 수 있으나, React상에 곧바로 적용시키기 애매한 경우가 있다.  
이때는 다음과 같은 방법을 사용하면 된다

# Code

두가지 방법이 있을 수 있다.

## html-react-parser 사용하기

```js
import Parser from "html-react-parser";

const text = "<div>blah</div>";
const makdDiv = () => {
  return <div>{Parser(text)}</div>;
};
```

## dangerouslySetInnerHTML 사용하기

```js
const text = "<div>blah</div>";
const makdDiv = () => {
  return <div dangerouslySetInnerHTML={{ __html: text }} />;
};
```

처음엔 위의 방법을 사용했었지만, 작동되지 않는 패턴이 발견되었음. 밑의 방법을 사용하기를 권장.
