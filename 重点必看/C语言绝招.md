# 两个口诀核心！！！

变量变量，能变，就是能读能写，必然存在内存中

指针指针，保存的就是地址，在32位处理器中，地址都是32位的，不论是什么变量，都是4字节

# 变量 && 指针

什么是变量，什么是指针呢？变量变量，可读可写，能改变的就是变量，那么指针是存储变量地址的变量![image-20250115180001188](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250115180001188.png)

为什么char 类型的变量大小是1，char 类型的指针大小是4字节呢，因为char中存储的是一个字符，而一个字符的大小就是1 ，而指针中存储的是地址，在32位处理器 





# sizeof 跟关键字

## const 只读变量放在哪里？

当变量增加了const 的时候，是被放在flash 上面的，用于节省内存



## 如何知道指针占用内存大小？

举个例子，如果我们想知道int a  a变量占用内存的大小,那么我们只需要sizeof（a）就可以的，显而易见的，想知道变量的大小，就要通过变量名来获取，而int* p 的变量名就是P 而如果是sizeof(*p)，那么查找的就是 int 类型所占用的空间

所以sizeof (*p)的大小是4，这里代表的是32位的int 类型的大小，而 sizeof(p) 求的是 int * 这个指针的大小，而在x86(32位)和x64(64位) 系统上，指针大小又有所不同，因为指针指向的是地址的大小



## static volatile 的作用

在我们工作中，不同的库文件中，可能会有名字相同的变量，所以可以加上static 限制作用域

而volatile 表示不要优化代码，表示变量是异变的

![image-20250115195821932](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250115195821932.png)

## extern 的作用

externa到底在哪里用

比如main文件要使用 delay.c 中的int a 变量，那么只需要在main 文件中extern int a;就可以了，可以在main.c里面写，也可以在delay.h包含的头文件里面写，main.c进行调用，只需要让使用者知道就好了

![image-20250115195655719](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250115195655719.png)

## struct 引入结构体赋值 

struct wei{	

​	char * name;

​	int num;

}

struct wei = {"张三",188}

取出对象wei.name

这种类型占用空间吗，不占，只有变量才会占用空间，类型是不占用空间的   

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250115201048286.png" alt="image-20250115201048286" style="zoom:25%;" />

为什么这里都是8个字节   

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20250115201454749.png" alt="image-20250115201454749" style="zoom:25%;" />

因为虽然这里的char类型就占用一个字节，但是他还是会以4个字节的空间进行跳跃，另外如果是

struct wei{	

​	char name;

​	char class;

​	int num;

}

通过int 类型的指针，对char 类型的数据进行改写的话，就会造成class 的数据被覆盖

## 函数指针

```
#include <stdio.h>

// 定义两个不同的Logo绘制函数
void drawLogoA() {
    printf("Drawing Logo A\n");
}

void drawLogoB() {
    printf("Drawing Logo B\n");
}

// 定义 lcd_operation 结构体
typedef struct lcd_operation {
    int type;                // 屏幕类型
    void (*drawlogo)(void);  // 函数指针，指向绘制Logo的函数
} lcd_operation, *p_lcd_operation;  // p_lcd_operation 是指向 lcd_operation 结构体的指针类型

// 假设的 get_lcd_type 函数，返回屏幕类型
int get_lcd_type() {
    // 这里可以是读取EEPROM或其他配置的代码
    // 为了示例，假设返回 0 表示屏幕A，1 表示屏幕B
    return 0;  // 或者 return 1;
}

// 定义一个 lcd_operation 结构体数组
lcd_operation xxx_com_lcds[] = {
    {0, drawLogoA},  // 屏幕A，使用 drawLogoA 函数
    {1, drawLogoB}   // 屏幕B，使用 drawLogoB 函数
};

// get_lcd 函数，返回指向 lcd_operation 结构体的指针
p_lcd_operation get_lcd(void) {
    int type = get_lcd_type();  // 获取当前屏幕类型
    return &xxx_com_lcds[type]; // 返回对应屏幕类型的 lcd_operation 结构体指针
}

int main() {
    // 获取当前屏幕的操作结构体指针
    p_lcd_operation currentScreen = get_lcd();

    // 调用当前屏幕的绘制Logo函数
    currentScreen->drawlogo();

    return 0;
}
```

## typedef 

用于重命名类型



# 链表操作

```
typedef struct spy 
{
	char* name;
	struct spy *next;
}spy,*p_spy;

/*事实上，这里的结构体指针，如果没有typedef 的话就表现为
 *strcut spy *p_syp
 */

spy A = {"A",NULL};
spy B = {"B",NULL};
spy C = {"C",NULL};

A.next = &B;
B.next = &C;
C.next = NULL;
```

## 链表的插入与删除

首先，链表的插入分为两种情况，一种就是链表为空，那么头部指向地址，就是插入的第一个元素的地址，如果链表有东西，就需要在加上一个尾部指针，首先，先让尾部指针移动到头部指针的位置，而头部指针位置永远都是第一个元素，然后，判断尾部指针指向元素的next 是否为空，如果为空就说明找到链表的最后一个元素了，就将链表的最后一个元素的next 指向 新添加的元素地址，然后将新添加元素的next 对象，设置为NULL，防止环形产生，如果不为空，就将尾部指针的位置，下移一位进行判断

## 链表的删除

如果我想要删除某一个元素，那么我就需要找到他的前一个跟后一个，然后，让左边的元素，指向右边，那么如何找到前一个呢，从头开始找，如果next 等于要删除的地址，那么就找到了

# 几个核心问题

- 全局变量的初始化
  - 类似memcpy，把FLash 上的数据段，整体拷贝到RAM
- 初始值为0，没有初始化的全局变量，如何初始化？
  - 有100万个这样的没有初始化的变量
  - 全部放在flash中吗？
  - 把这些变量都放在ZI段
  - 类似于memset，把ZI段全部清0

- 才去调用main函数
- 全局变量在哪里
- 局部变量的初始化
  - 保存返回地址

- 栈的作用



首先在程序运行的时候，会将数据段重定位到RAM中，其中就是全局变量

其中没有初始化，以及初始化为0的变量，就会放在ZI段，进行集体初始化，



- 我们知道当设备断电之后，内存中是不会 存储的 ，那么全局变量初始值就来自于flash
- 如何设置他的初始值呢

​	当程序上电的时候，bin 文件中，有着数据段，跟代码段，那么程序上电的时候，数据段中的全局变量，就会移动到RAM中，每个全局变量都有着自己的地址，这就是重定位，三个关键就是，源、目的，以及长度