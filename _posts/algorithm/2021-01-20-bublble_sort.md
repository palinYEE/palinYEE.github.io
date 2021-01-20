---
layout: post
title:  "[Algorithm] 버블 정렬 (bubble Sort)"
date:   2021-01-20T10:00:52-05:00
author: 윤영진
categories: algorithm 
tags: algorithm sorting
cover:  "/assets/instacode.png"
---
# 선택 정렬 (Selection Sort)

* 공부 날짜 : 2021-01-20 오후 10시

![Alt text](/assets/algorithm/2021-01-20_bubble_sort.png "필기")

### Code

```
#include<stdio.h>
#include<time.h>

int main(){
    int i, j, temp;
    clock_t start_time, end_time;
    int array[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};
    printf("[*] Lets sort array {1, 10, 5, 8, 7, 6, 4, 3, 2, 9} by using Bubble Sort \n");
    start_time = clock();
    for(int k=0; k<100000000; k++){
        for(i=0; i<10; i++){
            for(j=0; j<9-i; j++){
                if(array[j] > array[j+1]){
                    temp = array[j];
                    array[j] = array[j+1];
                    array[j+1] = temp;
                }
            }
        }
    }
    end_time = clock();
    printf("[*] Bubble Sort Result { ");
    for(i=0; i<10; i++){
        printf("%d, ", array[i]);
    }
    printf("}\n");


    printf("[*] total elapsed time : %d", (end_time-start_time)/1000);
    
}
```
