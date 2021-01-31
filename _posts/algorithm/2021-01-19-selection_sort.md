---
layout: post
title:  "[Algorithm] 선택 정렬 (Selection Sort)"
date:   2021-01-19T10:00:52-05:00
author: 윤영진
categories: algorithm 
tags: [algorithm, sorting]
cover:  "/assets/instacode.png"
---
# 선택 정렬 (Selection Sort)

* 공부 날짜 : 2021-01-19 오후 12시


![Alt text](/assets/algorithm/2021-01-19_select_sort.png "필기")

### Code

```

#include<stdio.h>

int main(){
    int i, j, min, index, temp;
    int array[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};

    for(i = 0; i < 10; i++){
        min = 9999;
        for(j = i; j < 10; j++){
            if(min > array[j]){
                min = array[j];
                index = j;
            }
        }
        temp = array[i];
        array[i] = array[index];
        array[index] = temp;
    }
    for(i=0; i<10; i++){
        printf("%d ", array[i]);
    }
    return 0;
}
```
