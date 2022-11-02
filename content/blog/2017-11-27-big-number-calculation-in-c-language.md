---
title: C语言 大数加法 减法 乘法
author: Q
type: post
date: 2017-11-27T14:36:45+00:00
url: /blog/902
wp_player_music_type:
  - netease
mp3_xiami_type:
  - song
wp_player_lyric_open:
  - close
toc_depth:
  - 1
i3geek_xzh_submit:
  - -1
views:
  - 2095
categories:
  - Programming
tags:
  - C

---

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

void stringReverse(char * p)//逆序字符串
{
    int i,len;
    char temp;
    len = strlen(p);

    for(i=0; i&lt;(len/2); i++)
    {
        temp = p[i];
        p[i] = p[len-1-i];
        p[len-1-i] = temp;
    }
}

char* getString()//动态字符串输入
{
    char *str;
    char *_str;
    int i=1;

    str=(char*)malloc(sizeof(char)*(i+1));

    while((str[i-1]=getchar())!='\n'){
        i+=1;

        _str=(char*)malloc(strlen(str)+1);
        str[i-1]='\0';

        strcpy(_str,str);
        free(str);

        str=(char*)malloc(sizeof(char)*(i+1));
        if(str==NULL){
            free(_str);
            printf("Not enough memory!");
            return NULL;
        }

        strcpy(str,_str);
        free(_str);
    }
    str[i-1]='\0';
    return str;
}

char* remove_0(char *c)//删除0
{
    char *temp,*ch;
    temp=c;
    while(*temp){
        if(*temp!='0') break;
        temp+=1;
    }

    ch=c;
    while(*temp){
        *ch=*temp;
        ch+=1;
        temp+=1;
    }
    *ch='\0';

    return c;
}

char* add(char *a,char *b)//加法
{
    char *c;
    char *ch1,*ch2,*ch3;
    int len=0;
    int i=0,j=0;
    int x=0,y=0;

    len = strlen(a)>=strlen(b) ? strlen(a) : strlen(b);

    c=(char*)malloc(sizeof(char)*(len+1));

    stringReverse(a);
    stringReverse(b);

    ch1=a;
    ch2=b;
    ch3=c;
    while(*ch1!='\0' || *ch2!='\0'){
        if(*ch1!='\0') i=*ch1-'0';
        if(*ch2!='\0') j=*ch2-'0';
        x=i+j+y;
        *ch3=(x%10)+'0';
        ch3+=1;
        y=x/10;
        if(*ch1!='\0') ch1+=1;
        if(*ch2!='\0') ch2+=1;
        i=0;
        j=0;
    }
    *ch3='\0';

    stringReverse(c);

    return c;
}


char* minus(char *a,char *b)//减法
{
    char *c;
    char *temp;
    char *ch1,*ch2,*ch3;
    int sign=0;
    int len=0;
    int i=0,j=0;
    int x=0,y=0;

    len = strlen(a)>=strlen(b) ? strlen(a) : strlen(b);

    c=(char*)malloc(sizeof(char)*len);

    if((strlen(a)==strlen(b) && strcmp(a,b)&lt;0) || strlen(a)&lt;strlen(b)){
        temp=a;
        a=b;
        b=temp;
        sign=1;
    }

    stringReverse(a);
    stringReverse(b);

    ch1=a;
    ch2=b;
    ch3=c;
    while(*ch1!='\0' || *ch2!='\0'){
        if(*ch1!='\0') i=*ch1-'0';
        if(*ch2!='\0') j=*ch2-'0';
        x=i-j-y;
        if(x&lt;0){
            y=1;
            x+=10;
        }else{
            y=0;
        }
        *ch3=(x%10)+'0';
        ch3+=1;
        if(*ch1!='\0') ch1+=1;
        if(*ch2!='\0') ch2+=1;
        i=0;
        j=0;
    }
    *ch3='\0';

    stringReverse(c);

    remove_0(c);

    if(sign==0){
        return c;
    }else{
        printf("-");
        return c;
    }
}


char* by(char *a,char *b)//乘法
{
    char *c;
    int len=0;
    int temp=0;
    int i=0,j=0;
    int x=0,y=0;

    len=strlen(a)+strlen(b);

    stringReverse(a);
    stringReverse(b);

    c=(char*)malloc(sizeof(char)*(len+1));
    memset(c,0,sizeof(char)*(len+1));

    for(i=0;i&lt;strlen(b);i+=1){
        for(j=0;j&lt;strlen(a);j+=1){
            x=a[j]-'0';
            y=b[i]-'0';
            temp=x*y;
            c[i+j]+=temp;
        }
    }

    x=0;
    for(i=0;i&lt;len;i+=1){
        c[i]+=x;
        x=c[i]/10;
        c[i]%=10;
    }

    for(i=0;i&lt;len;i+=1){
        c[i]+='0';
    }

    stringReverse(c);

    remove_0(c);

    return c;
}

int main(){
    char *a,*b,*operator;

    printf("Infinite Positive Integer Operation\n");
    printf("-----------------------\n");

    printf("Please enter the first positive integer:\n");
    a=getString();

    printf("Please enter the operator(+ - * /):\n");
    operator=getString();

    printf("Please enter the second positive integer:\n");
    b=getString();

    printf("The result is:\n");

    switch (*operator){
        case '+':
            puts(add(a,b));
            break;
        case '-':
            puts(minus(a,b));
            break;
        case '*':
            puts(by(a,b));
            break;
            /*case '/':
                puts(divide(a,b));
                break;*/
        default:
            printf("error");
            break;
    }


    return 0;
}
```