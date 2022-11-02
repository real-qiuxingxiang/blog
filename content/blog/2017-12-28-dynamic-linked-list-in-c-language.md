---
title: C语言 动态创建链表 Linked List
author: Q
type: post
date: 2017-12-28T05:46:56+00:00
url: /blog/914
views:
  - 1481
categories:
  - Programming
tags:
  - C

---

```c
#include <stdio.h>
#include <stdlib.h>

typedef struct LinkedListNode
{
    int data;
    struct LinkedListNode *next;
} NODE;

NODE *creatList(int n, int m)
{
    NODE *temp=NULL;
    NODE *origin;
    NODE *extend;

    origin=(NODE*)malloc(sizeof(NODE));
    temp=origin;
    origin->next=NULL;

    for(int i=1;i&lt;=n;i+=1){
        extend=(NODE*)malloc(sizeof(NODE));
        extend->data=i;
        extend->next=origin->next;
        origin->next=extend;
        origin=origin->next;
    }
    return temp;
}

void outputLink(NODE *head)
{
    NODE *temp;
    temp=head->next;

    printf("HEAD");
    while(temp){
        printf("->%d",temp->data);
        temp=temp->next;
    }
}

int main() {
    NODE *head;
    head=creatList(10,10);
    outputLink(head);
    return 0;
}
```