---
layout: post
title:  "[Algorithm] 알고리즘 문제 풀이 1"
date:   2021-01-26T10:00:52-05:00
author: 윤영진
categories: algorithm 
tags: algorithm sorting
cover:  "/assets/instacode.png"
---
# 알고리즘 문제 풀이

* 공부 날짜 : 2021-01-25 ~ 2021-01-26 (25일에는 너무 피곤해서 한문제만 풀고 잤다...)

# code

(https://www.acmicpc.net/problem/2752)

```
#include<stdio.h>

int main(){
    int i, j, min, index, temp;

    int array[3];

    scanf("%d %d %d", &array[0], &array[1], &array[2]);
    for(i=0;i<3;i++){
        min = 1000000;
        for(j=i; j<3; j++){
            if(min > array[j]){
                min = array[j];
                index = j;
            }
        }
        temp = array[i];
        array[i] = array[index];
        array[index] = temp;
    }

    for(i=0; i<3; i++){
        printf("%d ",array[i]);
    }
    return 0;
}
```

* (https://www.acmicpc.net/problem/2750)

```
#include<stdio.h>
#include<stdlib.h>

void quickSort(int* data, int start, int end){
    if(start > end){
        return;
    }

    int key = start;
    int i = start+1, j = end, temp;

    while(i <= j){
        while(i<=end && data[i] <= data[key]){
            i++;
        }
        while(j > start && data[j] > data[key]){
            j--;
        }
        if(i>j){
            temp = data[j];
            data[j] = data[key];
            data[key] = temp;
        }else{
            temp = data[i];
            data[i] = data[j];
            data[j] = temp;
        }
    }
    quickSort(data, start, j-1);
    quickSort(data, j+1, end);
}

int main(){
    int N;
    int data[1001];
        
    scanf("%d", &N);
    for(int i=0; i<N; i++){
        scanf("%d", &data[i]);
    }
    quickSort(data, 0, N-1);
    
    for(int i=0; i<N; i++){
        printf("%d\n", data[i]);
    }
}
```

* (https://www.acmicpc.net/problem/2751)

```
#include<stdio.h>
#include<algorithm>

int number, array[1000000];

int main(){
    scanf("%d", &number);
    for(int i=0; i<number; i++){
        scanf("%d", &array[i]);
    }

    std::sort(array, array+number);

    for(int i=0; i<number; i++){
        printf("%d\n", array[i]);
    }
}
```

c++의 `std::sort` 함수는 위대하다...