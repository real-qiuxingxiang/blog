---
title: C语言 扫雷
author: Q
type: post
date: 2017-09-04T03:44:42+00:00
url: /blog/890
views:
  - 1509
categories:
  - Programming
tags:
  - C

---
Minesweeper in C

C语言扫雷

9*9

可以自动消除一大片

代码如下：

```c
#include <stdio.h>
#include <stdlib.h>
#include <time.h>

#define N 9 //9*9扫雷

int sum = 10; //雷数目
int mine[N][N] = {0}; //雷数组
int map[N][N]; //显示数组
int markDirection[8][2] = {{0,1},{1,1},{1,0},{1,-1},{0,-1},{-1,-1},{-1,0},{-1,1}}; //8个方向

void printMap() //打印地图
{
    int i = 0,j = 0;
    for(i=0;i&lt;N;i++)
    {
        for(j=0;j&lt;N;j++)
        {
            printf("%d ",map[i][j]);
        }
        printf("\n");
    }
}

void setMine() //埋雷
{
    srand((int)time(0));
    int x=0,y=0;

    while(sum >= 0)
    {
        x = (rand()%(9-1+1))+1;
        y = (rand()%(9-1+1))+1;

        if(mine[x][y] != 1)
        {
            mine[x][y] = 1;
            sum -= 1;
        }
    }
}

int countMine(int x,int y) //数雷
{
    int count=0;
    int x1 = 0, y1 = 0;
    int i = 0;
    
    for(i=0;i&lt;N;i++)
    {
        x1 = x + markDirection[i][0];
        y1 = y + markDirection[i][1];
        if(x1&lt;0 || x1>=N || y1&lt;0 || y1>=N) continue;
        if(mine[x1][y1] == 1) count += 1;
    }
    return count;
}

void autoClear(int x,int y) //自动消一大片
{
    int x1 = 0, y1 = 0;
    int i = 0;
    int count = 0;
    
    map[x][y] = 0;
    
    for(i=0;i&lt;N;i++)
    {
        x1 = x + markDirection[i][0];
        y1 = y + markDirection[i][1];
        if(x1&lt;0 || x1>=N || y1&lt;0 || y1>=N) continue;
        count = countMine(x1,y1);
        if(count != 0) 
        {
            map[x1][y1] = count;
        }else if(map[x1][y1]==0){
            continue;
        }else{
            autoClear(x1,y1);
        }
    }
}

int winCheck() //赢了吗
{
    int count = 0;
    int i=0,j=0;
    
    for(i=0;i&lt;N;i++)
    {
        for(j=0;j&lt;N;j++)
        {
            if(map[i][j] == 9) count += 1;
        }
    }
    if(count == sum)
    {
        return 1;
    }else{
        return 0;
    }
}

void Gameover() //炸了
{
    int i = 0,j = 0;
    for(i=0;i&lt;N;i++)
    {
        for(j=0;j&lt;N;j++)
        {
            printf("%d ",mine[i][j]);
        }
        printf("\n");
    }
}

int main()
{
    int X=0,Y=0;
    int i=0,j=0;
    int check=0;
    int result = 1;
    
    for(i=0;i&lt;N;i++)
    {
        for(j=0;j&lt;N;j++)
        {
            map[i][j] = 9;
        }
    }
        

    
    printf("*********扫雷**********\n");
    printMap();
    setMine();
    
    while(result)
    {
        printf("输入 行,列\n");
        scanf("%d,%d",&X,&Y);
        
        X -= 1;
        Y -= 1;
        
        if(mine[X][Y] == 1)
        {
            printf("Game over!\n");
            Gameover();
            result = 0;
        }else{
            check = countMine(X,Y);
            if(check != 0)
            {
                map[X][Y] = check;
            }else{
                autoClear(X,Y);
            }
            printMap();
        }
        
        if(winCheck())
        {
            printf("You win!");
            break;
        }
        
    }
    return 0;
}
```

代码：<https://github.com/real-qiuxingxiang/Minesweeper-C>