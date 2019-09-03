---
layout: post
title: "Combination/Permutation"
date:   2019-08-09 21:24:10 +0900
categories: #cpp #stl
---

# Combination
---
## 구현 방법
자주 사용되는 기법으로는 for문 중첩, 재귀 방식이 있다.   
for문 중첩으로는 4개 이상은 아무래도 코드상 무리가 있기 때문에 보통 재귀방식을 선호.


### Code (6C3 구현)
#### 재귀
~~~cpp
// 목표 :  6C3을 구현 
int m = 3; // nCm에서 m
int temp[3]
// 조합의 기본은 꺼내 담은 위치의 다음 위치를 바라보는것
void combination(int* arr, int depth, int p) {
    if(depth == m) {
        print(arr);
        return;
    }
    // 여기서 4 + depth는 arr의 개수가 6개 이기 때문 
    for (int i = p ; i < 4 + depth; i++) {
        temp[depth] = arr[i];
        combination(arr, depth + 1, i+1);
    }
}

~~~

#### for문 중첩
~~~cpp 
//로직상 위의 재귀와 다를바가 없으나 코드가 좀 더럽다
// 다만 2~3개의 조합을 원할 때 이 방식도 나쁘지 않다. 
void combination2(int * arr) {
    for (int i = 0; i < 4; i++) {
        for (int j = i + 1; j < 5; j++) {
            for (int k = j + 1; k < 6; k++) {
                int temp[3];
                temp[0] = arr[i];temp[1] = arr[j]; temp[2] = arr[k];
                print(temp);
            }
        }
    }
}
~~~

# Permutation
### 순열

다양한 방법이 있는 듯 하지만, 이 방법이 가장 마음에 드는것 같다.



~~~cpp

void per(int* arr, int depth){
    if(depth == 3) {
        print(arr);
        return;
    }
    for (int i = depth; i < 3; ++i) {
        swap(arr[i], arr[depth]);
        per(arr, depth + 1);
        swap(arr[i], arr[depth]);
    }
}
~~~


