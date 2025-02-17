# FreeRTOS的编程风格

## 数据类型

```c
#define portCHAR        char
#define portFLOAT       float
#define portDOUBLE      double
#define portLONG        long
#define portSHORT       short
#define portSTACK_TYPE  uint32_t
#define portBASE_TYPE   long

typedef portSTACK_TYPE StackType_t;
typedef long BaseType_t;
typedef unsigned long UBaseType_t;

#if( config USE_16_BIT_TICKS == 1 )
typedef uint16_t TickType_t;
#define portMAX_DELAY ( TickType_t ) 0xffff
#else
typedef uint32_t TickType_t;
#define portMAX_DELAY 
 TickType_t ) 0xffffffffUL
```

## 变量名

char  前缀c

short 前缀 s

long 前缀 l

portBASE_TYPE 前缀x

无符号型 前缀u

指针变量 前缀 p

## 函数名

函数名包含函数返回值类型、函数所在的文件名和函数的功能

私有函数会加一个prv(private)前缀

1）vTaskPrioritySet()函数的返回值为void型，在task.c文件中定义。
	2）xQueueReceive()函数的返回值为portBASE_TYPE型，在queue.c文件中定义。
	3）vSemaphoreCreateBinary()函数的返回值为void型，在semphr.h文件中定义。

## 函数名

宏均由大写字母表示，并配有小写字母前缀，前缀用于表示该宏在哪个头文件定义

![f71d9db2328704fbc08003f61c5f655](https://raw.githubusercontent.com/remfoever/md_image_repo/main/f71d9db2328704fbc08003f61c5f655-1739616013833-4.jpg)

通用宏定义

![8e897d9a9d0c98a7f9f67086c02cd6d](https://raw.githubusercontent.com/remfoever/md_image_repo/main/8e897d9a9d0c98a7f9f67086c02cd6d.jpg)

## 格式

1个Tab键等于4个空格键，编程时最好使用空格键，当两个编译器的Tab键大小设置不一样时移植代码格式会变乱，使用空格就不会出现这种问题。











