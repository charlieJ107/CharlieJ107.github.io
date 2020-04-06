# 重读C Primer Plus( 2 )

## 指针

​	为什么我要先说指针?

​	因为指针对于C语言来说太重要了. 最令人绝望的是, 指针在很多场合下的使用频率总是在被以往和熟练之间的分界线上. 所以每次用到时, 似乎记得, 又不太熟悉. 

​	所以, 我决定先把指针记下来, 以备查阅. 

### 指针变量

1. 指针就是地址！

2. 取地址符：

   ```c
   &
   ```

   一般来说第一次接触它应该是在scanf里面, 这个运算符的作用就是获得后面跟着的变量的地址. 所以, 如果指针变量名是ptr (pointer的缩写) ,就可以编写如下的语句:

   ```c
   ptr=&pooh;//把pooh的地址赋给ptr
   ```

   对于这条语句, 我们说ptr是指向pooh的. 

3. 间接运算符:

   ```c
   *
   ```

   一般来说意思是"取内容", 与之前那个"取地址"相区分. 

4. 指针的声明

   指针的声明必须声明指针的类型. 

   ```c
   int * pi;
   char * pc;
   float * pf, * pg;
   ```

   *和指针名之间的空格可有可无, 通常, 程序员在声明时使用空格, 在解引用变量的时候省略空格. 

   

### 用指针在函数间通信

示例代码:

```c
#include <stdio.h>
void interchange(int * u, int * v);

int main(void)
{
    int x =5, y = 10;
    printf("Originally x = %d and y = %d. \n",x, y);
    intengerchange(&x, &y);//把地址发送给函数
    printf("Now, x =% d and y = %d .\n",x,y);
    
    return 0;
}

void interchange(int * u, int * v)
{
    int temp;
    temp= *u;//temp获得U所指向的对象的值
    *u = *v;
    *v = temp;
}
```

