---
layout: post
title:  "Redux-input 사용 시 캐릭터 하나만 입력해도 re-rendering 되는 경우"
date:   2019-11-22 13:50:10 +0900
categories: #react #redux #js
---

# Issue
 
Redux의 state를 구독한 상태의 input에 값을 입력 시 한글자만 입력해도 리랜더링이 일어남

문제 Code

~~~js
const TextInput = ({ value, onChange }) => {
  const Input = styled.input`
    height: auto;
    line-height: normal;
    padding: 0.1em 0.5em;
    width: 85%;
  `;
  return (
    <Input
      type="text"
      value={value.val}
      onChange={e =>
        onChange({
          id: value.id,
          input: e.target.value,
        })
      }
    />
  );
};
~~~

해결책

~~~js
const Input = styled.input`
    height: auto;
    line-height: normal;
    padding: 0.1em 0.5em;
    width: 85%;
  `;
const TextInput = ({ value, onChange }) => {
  
  return (
    <Input
      type="text"
      value={value.val}
      onChange={e =>
        onChange({
          id: value.id,
          input: e.target.value,
        })
      }
    />
  );
~~~

# 원인 분석/고찰

## 원인
TextInput 함수 내에 있었기 때문에, 값이 바뀔 때 마다 Input이 재정의 되게 된다.

## 고찰
지금 생각해보면 매우 멍청한 실수지만, 동적으로 Input을 조절할 이유가 있었던 선례가 있었기 떄문에 실수가 나왔다.

다음부터는 함수의 용도에 맞게 작성 할 수 있도록 하자.
