---
layout: post
title:  "[Algorithm] 퀵 정렬 (Quick Sort)"
date:   2021-01-24T10:00:52-05:00
author: 윤영진
categories: algorithm 
tags: algorithm sorting
cover:  "/assets/instacode.png"
---
# 퀵 정렬 (Quick Sort)

* 공부 날짜 : 2021-01-24 오후 10시

![Alt text](/assets/algorithm/2021-01-24_quicksort.jpg "필기")

### Code

#### 오름차순

```
#include<stdio.h>

int number = 10;
int data[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};

void show(){
    printf("Finish quick sort\n");

    for(int i=0; i<number; i++){
        printf("%d ", data[i]);
    }
}

void quickSort(int* data, int start, int end){
    if(start > end){ // 원소가 1개 남거나 피벗보다 작은 값이 없을 경우 멈추는 코드
        return;
    }

    int key = start;
    int i = start+1, j = end, temp;

    while(i <= j){
        while(i <= end && data[i] <= data[key]){ // 피벗 보다 큰 값의 index를 찾는 부분
            i++;
        }
        while(j > start && data[j] > data[key]){ // 피벗 보다 작은 값의 index를 찾는 부분
            j--;
        }
        if(i > j){
            temp = data[key];
            data[key] = data[j];
            data[j] = temp;
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
    printf("start quick sort\n");
    quickSort(data, 0, number-1);
    show();
    return 0;
}
```

#### 내림차순

```
#include<stdio.h>

int number = 10;
int data[10] = {1, 10, 5, 8, 7, 6, 4, 3, 2, 9};

void show(){
    // printf("Finish quick sort\n");

    for(int i=0; i<number; i++){
        printf("%d ", data[i]);
    }
    printf("\n");
}

void quickSort_dec(int* data, int start, int end){
    if(start > end){
        return;
    }

    int key = start;
    int i=start+1, j=end, temp;

    while(i <= j){
        while(i <= end && data[i] >= data[key]){
            i++;
        }
        while(j > start && data[j] < data[key]){
            j--;
        }
        if(i>j){
            temp = data[key];
            data[key] = data[j];
            data[j] = temp;
        }else{
            temp = data[i];
            data[i] = data[j];
            data[j] = temp;
        }
        
    }
    show();
    quickSort_dec(data, start, j-1);
    quickSort_dec(data, j+1, end);
}

int main(){
    quickSort_dec(data, 0, number-1);
    show();
    return 0;
}
```