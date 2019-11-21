---
layout: post
title:  "Redux-Action사용시-parameter-여러개 입력하는 방법"
date:   2019-11-15 13:50:10 +0900
categories: #react #redux #js
---

# 하나는 잘들어가는데 여러개가 안들어가!!

Action도 잘만들고 함수도 잘 가져왔는데 데이터가 안넘어온다.
~~~js
    export const setProps = createAction(SET_PROPS, ({ proplist, classattrs }) => ({
        proplist,
        classattrs,
    }));

    [SET_PROPS]: (state, { payload: { proplist, classattrs } }) => {
      return {
        ...state,
        values: proplist,
      };
    }

    // 이 코드에서는 classatters가 사용되지는 않았으나 필요로 한다.
~~~

별 이상이 없다. 다만 받아오는 함수에서 적절히 처리해 주기 위해서는 

~~~js
    return setProps({
        proplist: attrList[clazz.className],
        classattrs: clazz['attr'],
    });
~~~

이런 식으로 객체를 만들어 보내주어야 한다. 

이유는 받아오는 함수가 Action.payload(객체) 를 통해 받아오게 되는데

여러 argument를 전달 시 데이터 매핑을 해 주어야 하기 때문에 제대로 받아오지를 못한다

하나의 경우 어차피 하나라서 받아올 수 있게 된 것 같다.
