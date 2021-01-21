---
layout: post
title:  "[Algorithm] 삽입 정렬 (Insertion Sort)"
date:   2021-01-21T20:52-05:00
author: 윤영진
categories: algorithm 
tags: algorithm sorting
cover:  "/assets/instacode.png"
---
# 삽입 정렬 (Insertion Sort)

* 공부 날짜 : 2021-01-21 오후 8시

![Alt text](/assets/algorithm/2021-01-21_insertion_sort.png "필기")

### Code

```
#include<stdio.h>

int main(){
    int i, j, temp;
    int array[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};
    printf("Start insertion sort example\n");

    for(i=0; i<10; i++){
        j=i;
        while (array[j] > array[j+1]){
            temp = array[j];
            array[j] = array[j+1];
            array[j+1] = temp;
            j--;
            if(j<0){
                break;
            }
        }
        
    }

    printf("Finish insertion sort example : ");
    for(i=0; i<10; i++){
        printf("%d ", array[i]);
    }

}
```
