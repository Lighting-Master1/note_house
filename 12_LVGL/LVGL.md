# lvgl 缩写大全

对象（lv_obj_t）

# 基础对象（lv_obj）

## 基础对象的简介

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NzM1YzlmM2U2Y2NhYTkwZjNmNmE3YmU1Y2E5MjFiYzVfalFYNWlkcWJ2cmtuVTBaNTRmNjJxY2tHUWhLdjdERUtfVG9rZW46Tmd3ZmJMYkVlb3kwdXZ4MUphUWNnbTllbmhkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjlhZjkwMjc5NmU4MGU3YmM3MDUyMGVjNjA0ZTNhMmVfY1JkamtvVmszMU56M00wdE83N2lUSU4wVU90a2VQWVZfVG9rZW46U0xrd2JSbXZqb2RLYXV4NDFTV2NtSUg0bnRnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTAxZDQxNzk4MGQzMTU1NzNjNTI5NDc0NmFjOTBjZWRfYnRFeHpFdmdHT1ZlWWhVZHFKUEJRMlBhNXFjbGlLSVhfVG9rZW46T3pBOWJtTHBwb0x3SkJ4M2RqTmNrWjRLbm1kXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

首先打开demo 工程，可以看到这么几个函数,那么他的运行效果就是下图

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDk5YWRiMDVmY2E0NTU5MTQxODNlNDI0ZDM1NDA0YWFfZXJQbktoaVIwT1prb09sd3NUMzgwcU4wUDlsYUhLRHVfVG9rZW46Wm9Ja2J1YTFhb2dHM2x4Z3drbGN4aWVkbnVlXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2UyZWJiYmY4Mzg0ODcxMDY0MDRlYjBkMTI0OTE5MTlfMUdxa3RXaVZ1RXpzVVNySm12eXB0dHEyeUkwQTVMaHhfVG9rZW46THh0NGIxRU5vb3BXWll4YWtaUWNDMnlkbmNmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

将所有的参数删除之后呢，就得到了一个基础对象

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjkyYWI4MGY1MGI1Mjg4ZGExY2YyNTY3ZTUyMDUyOWFfdk1CMUs1RUlONjZrNjRaMnI1MlgxeEluNmU1WHJqQVdfVG9rZW46UVBNR2JCNUF5b2Q1Mmp4YUlUb2N2VXJDbkRlXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MjM0MzZkNDFjZDU0ZDM2NGEyY2E5NGRkNjFlMzMxMDNfS05mUlFTWU80dnMzQXZ0WXloUDZxV3RNMkVNZWtkeFBfVG9rZW46S3JlY2JrbkJBb1prS0J4bGowaGNWQWRJbkNnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

```Plain
    lv_obj_t * obj = lv_obj_create(lv_scr_act());
    这段代码的作用就是创建一个对象，
    他的父级是屏幕 通过lv_scr_act()这个参数进行指定
    lv_obj_set_size(obj, LV_PCT(20), LV_PCT(10));
    lv_obj_set_size(obj, LV_PCT(40), LV_PCT(20));
    lv_obj_align(obj, LV_ALIGN_CENTER, 0, 0);

    lv_obj_t * label = lv_label_create(obj);
    lv_label_set_text_fmt(label, "Hello, LVGL!\nLVGL V%d.%d.%d\nhttps://www.100ask.net", lv_version_major(), lv_version_minor(), lv_version_patch());
    lv_obj_align(label, LV_ALIGN_CENTER, 0, 0);
```

lv_obj_create()

创建基础对象

lv_obj_create(lv_scr_act());

screen屏幕 active就是活动的意思

用于指定在当前屏幕上，进行组件的创建

lv_obj_align（）

Align的意思就是使一致，使对其的意思

例子：

lv_obj_align (label, LV_ALIGN_CENTER, 0, 0);

“label” 是要进行对齐操作的对象。

“LV_ALIGN_CENTER” 表示将对象在水平和垂直方向上都对齐到父级对象的中心位置。

Centier 中心线

### lv_obj_set_size

lv_obj_set_size(obj, LV_PCT(20), LV_PCT(10));

## 屏幕对象的创建过程

  lv_obj_t * obj = lv_obj_create(lv_scr_act());

那么这里的父类他是怎么被创建的呢(lv_scr_act) 这个屏幕的父类是如何被创建的呢，他只有被实例化之后，才可以被我们的组件使用

**屏幕实际上就是一个没有父类的基础对象**，在lv_hal_disp.c文件里我们可以看到，对于lv_obj_create 有两种处理方式，一种当屏幕已经存在的时候，就会创建对象，否则创建四个点

，用于确定屏幕的范围

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MzZhY2MyNmY4NjZkYWUxNzI3ZjM0NWExYmRhMzE0NjdfUXA4ZVBwTWk0RUJOdThjelZ0ZEFVbk95WkF4YlN6aFpfVG9rZW46SUdPSmI1WHZ6b2FsdU54OWNEZGNoYXJkbk1nXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

在 LVGL 中，屏幕对象创建过程大致如下：首先初始化库，然后注册显示器驱动。接着创建一个默认屏幕对象，并设置其坐标覆盖整个显示器的显示区域，从而为后续在该屏幕上添加各种 UI 元素做准备。

### Lvgl 的三层屏幕

我们一般只操作活动屏幕，你需要的组件多放在这里，顶层是用于存放错误的弹窗信息，而系统层就是我们鼠标等控件所存在的位置，所以不会受到其他组件的影响，这里我们一般不会用它

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OGM4ZTIwMGFiMGIyOTI4NTliNTZkMDdiMjEzODAzNDRfY1pBUzB4WXJDMDBERFI4OUIzZExZZk8xY3d6VXNDVE9fVG9rZW46Wkd2aWJpalNubzZVc3h4dGxuNGNydHViblllXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 基础对象的大小

要求，学会基础大小的获取，以及改变

void lv_obj_set_width(lv_obj_t * obj, lv_coord_t w);

void lv_obj_set_height(lv_obj_t * obj, lv_coord_t h);

void lv_obj_set_size(lv_obj_t * obj, lv_coord_t w, lv_coord_t h);

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=N2QxMTExZjRlNjZiN2Q1ZGM2ZjQ5MTRhYjBiZTQxNzlfS2IzQXk5enlmdnFiWFdNdDZpaEhiZEl0SGViSVRZNVVfVG9rZW46QmRUTGJ6bE5qb1lMWkZ4N1hCZGNZUmx1bjNiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 获取对象的大小

#### lv_obj_get_width(const lv_obj_t * obj);

#### lv_obj_get_height(const lv_obj_t * obj);

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjdiODRjZTdlZjRlYjNkY2JhYWM3YjA1NTA5N2M3ZjFfa1g4Z2dGdkFEME9Db1dTZEVJYjdMcVI0dDUzSElkeTJfVG9rZW46UVpaSmIxQXRlb3NPaFN4UzZSamN1eVFFbmRlXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 基础对象的位置

设置x轴坐标位置：

Iv_obj_set_x(obj, new_x);

 设置y轴坐标位置:

Iv_obj_set_y(obj, new_y);

同时设置x、y坐标位置：

Iv_obj_set_pos(obj, new_x, new_y); // position

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzU5YzIxZjI4Y2ZhNzY2N2MzNWFkNTgyNmIzNTM1MmJfUnN1ODc4SDdvZkNkbWpFWXdzWTlmZVNDV29MUWpnQ1JfVG9rZW46Q2paMWJKSXk1b1NkZ3p4MzB5SGNTbG5vbkxqXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 基础对象的对齐

这里的父级，其实就是我们的屏幕

lv_obj_set_align(obj, LV_ALIGN_...);

lv_obj_align(obj, LV_ALIGN_..., x, y);

lv_obj_align_to(obj_to_align, obj_referece, LV_ALIGN_..., x, y)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2M5MThlNWJlMmJkMGZmMjczODhhMTVlZGVkOGQ1NDFfVGJJNEt6cWdIME9TcHMxb0l6WUxnYkV5eWFJM21ueUdfVG9rZW46TFlEQmJMYmZtbzNyN3N4cERnYmNic2xlbkJnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 基础对象的对齐类型

他其实就是一个枚举类型，我们光看代码的话非常难以理解，这张图就很形象了

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTc5ZWU1OTU2YWE2NDU2MTRhOGRhNzZiOTVkMjM5MjJfSDF3QjhDaUpxTDFuSTl3dnhLeHlBVmZUUFNWTUs3NmFfVG9rZW46RzdZZ2JlNnN4b2FKMm14aHk1SGNudUR5blNkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDE2NjRlYjc3ZWE2NjY4MmUzMTUwNWZlMzk3MTdmM2JfWFk1cW1KbG5MZVI2c0ZOem4wZ01GblJ2cTYyRHQyV1RfVG9rZW46T0FnM2JZWlQ4bzFSUml4SE5uNmNrbHdqbjhkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 基础对象的获取位置

#### lv_obj_get_x(obj);

#### lv_obj_get_y(obj);

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDEyMmI5YzhiNzY2NmI3NmQxZDE1NGE1MGI3ZTI3YmZfRVM4enB4Y2JYUTJCQTFpZE5BV1FrU0llcmg3OEJoQThfVG9rZW46R2pyMWJxVEZsb05kTlR4V29mVmM2MVozbmpkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 基础对象的盒子

基础对象的盒子，分为了边界（bounding）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTJjZDE4YjMxMWEzNzgyMWQ2OGY2ZDU1MDFlZDBiNzNfMXdrTzRrblVzUkVRTDJGMjFQbUY2VmNSem1xblpOZUVfVG9rZW46V0UwUGJqUzRWb0NqMDB4c2pETmN4WEs3bkJoXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### CSS盒子模型

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Nzk5YzMxYjM0ZTc3MzdmNTUwZWExNDdhNTgzYWQ0NDVfWFNONFFHYjBTN200OEpmNGxYZFFRNDlobVZxa2QwQVhfVG9rZW46QnRaVmJmTmMyb3ZuVnp4TnBSbmNISnRhbnFmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDdkMzk4OGY1YmE5NWU0YWZjNjk4MjcwNmE5YjkzODVfa2Y1bHFPbXI3YjRCN1g4aUxlamJSOVdGSmlxR082Y0pfVG9rZW46Qzh2MWJNcnRFbzMzd094YmFtdGNVdlFVblhiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 基础对象的样式

样式的含义就是用名称保存下来的对修饰所使用的一组修饰参数

### 初始化样式

####         static lv_style_t style_obj;

####         lv_style_init(&style_obj);

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjNjYjY1YWJmMmVlZWYyZTJjODg5ZTIxYjc4YzlkZjdfNW5WZXB2T01TT2ROSUxBYjA5ZlNBZkc0N0k5bkF6WnNfVG9rZW46WjNaZ2JuV1VXb1F3bXh4Nmd0NmNBano4blViXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

初始化样式之后，是不会有任何的效果的，我们需要设置样式的属性

### 设置样式属性

#### lv_style_set_<property_name>(&style, <value>);

示例：        

lv_style_set_bg_color(&style_obj, lv_color_hex(0x000000));   // 设置背景色        lv_style_set_bg_opa(&style_obj, LV_OPA_50);                            // 设置背景透明度

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmNmMGY4YjkxYjRhN2VlYTFiZGM5ODAzMDU0OWE1NmVfU0wyTTVXUXpFd2gwQmRXNllwZkdSOXZQQkdBTjVHdXNfVG9rZW46R0l1R2JFUUZ0b09LUjd4dTNBN2NqbXJwbkZjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

设置完样式之后，他还是没有任何效果的，**需要将样式跟对象关联起来**，也就是添加样式到对象

### 添加样式到对象

lv_obj_add_style(obj, &style, <selector>)

lv_obj_add_style(obj, &style_obj, 0);       

lv_obj_add_style(obj, &style_obj, LV_STATE_PRESSED);  

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzAxYTU3YTUwZjYwM2VlMWI1ZDhhODhlMGQzNmNmMzFfeDFROVNFQjhoUjBSdFZEbmNvNjV3M0NiTDA4S0g1VGlfVG9rZW46VzNrZGJWZnl1b0llY0d4dXkzUGM4YXE2blZnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### **重点**  按下时显示样式

#### lv_obj_add_style(obj, &style_obj, 0);

这里0，所在位置，就是用于选择触发时事件，例如鼠标按下，聚焦等

### 源码讲解

那么我们这里给结构体传入这么多的属性，他都可以进行接收吗？

这里如果是一个样式他就会直接存储了，如果是多个样式的话，就会通过prop_cnt进行设置，然后传入数组

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MGE0MGNmZDUwNzM1ZTFhMDAwNmJhODU0ZGQ1OWM5NjRfZFNuWnVaaUVORjZaU2ZVRzNIS0Z2dGZWYmxXWTg1NDZfVG9rZW46UTJwS2I0MEQybzNPYUJ4YzQ2cmN2MGpSbkloXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 总结：添加样式到 对象需要四个步骤

暂时无法在飞书文档外展示此内容

## 样式部分和背景

### 状态（states）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGZjZTgzMDdjZWMzZTEzYmM5ZDhkNThiNjRmZTFmZmFfQm93QWtmNUpPRms4ell6VkNFeUdaNUlyYmRBbGFCVWFfVG9rZW46TXF0eWJjczZub0oyeFh4RWIwVmN5T2FYbnljXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 部分（parts）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YjVkM2Y4YmFjMzQ1NzY1MDIxMDM0OThmNzIyMWFiYzVfbUxJeVFwb3pySlU0Nkk3TnhSdFJNZDhOQThDRXg2M1FfVG9rZW46R044N2JZVlowb1NDeGh4NURyWmNOcXNMbkZjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

例：这里一共创建了四个样式，这里的lv_part_main就是对象的主要部分，如果我们单独执行这段的话就会发现，生成的只有一个矩形

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDJiMTEzNWZiMWRlMWJmYWI3YzY0MmZkNzJhYmJhY2VfRWxoSXF0YmU1QVZ6MTJnbFhlb0x1RzVtUVJWdndGRWRfVG9rZW46VjViemJzSWk1bzRZMHB4TUpHS2MyNlNCbkxjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### *重点

一个样式可以应用到多个样式上，同样的多个样式，也可以对一个对象进行操作

对象相同，样式不同

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTUwODBlNTQzZWQzZTFmOGY2YTQ5YWY3MmM5MzQ3YmNfOWtaNWRRV3lyZG1tZVM3dDE5d0t6dDdkcjhqMnEyTlJfVG9rZW46UXhUZGJnUTQyb0QzaHN4Ym9LUmNPcVdEbmliXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

样式相同，对象不同

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWQ4ZWMxNDIxY2FmMjczN2JjOWE3MjAwOGQ1ZmI0YThfTzZNMDg4TzM5RmRlR3lBYnFreTVETnlMdkZqcVhPSHpfVG9rZW46T3lXN2JtZVcyb0JPT3d4ZzJUeGNWcVVrbmNmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

另外还有一种样式，除了普通样式之外，对象还可以存储 本地样式

### 本地样式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjM1MDY4YzAxOTc4MzA1Yzk2MDBlYTRlYTg4MjY2ZjZfNFhZRnhhWmxDNFcwN0JCN2Z4TjU0bGpFU0k1NkR3VzBfVG9rZW46RFJzemJrb1Mzb1p1MXR4T3lVbmNOZEpMbnRlXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

例如这里的代码

```Plain
    lv_obj_set_style_bg_color(obj,  lv_color_hex(0x000000), LV_STATE_PRESSED);//设置背景颜色
    lv_obj_set_style_bg_opa(obj, LV_OPA_50, 0);//设置背景透明度
    
    删除样式
    lv_obj_remove_local_style_prop(obj, LV_STYLE_..., selector);
    LV_STYLE_...的取值请看： lvgl/src/misc/lv_style.h 中的 lv_style_prop_t 
```

他也可以实现按下的时候，改变对象的颜色

并且，同时设定了本地样式和普通样式的话，本地样式的优先级会高于普通样式，之后的内容还涉及到了，样式过度，样式主题与样式继承

### 样式继承

某些属性（通常与文本相关）可以从父对象的样式继承。 

只有没有在为对象设置样式属性的时候，才应用继承。 在这种情况下，如果这个属性是可继承的，那这个属性的值会在父类中检索，直到一个对象为该属性指定了一个值。父类将使用自己的状态来确定该值。 因此，如果按下按钮，并且文本颜色来自此处，则将使用按下的文本颜色。

### 过渡特效

默认情况下，当一个对象改变状态（例如它被按下）时，新状态的新属性会立即设置。但是，通过转换，可以在状态更改时播放动画。 例如，按下按钮时，其背景颜色可以在 300 毫秒内动画显示为按下的颜色。

### 样式主题

主题是风格的集合。如果存在活动主题，LVGL将其应用于每个创建的部件(对象)。 这将为UI提供一个默认外观，然后可以通过添加更多样式对其进行修改。

## 对象的事件（events）

什么是事件？我这里对于事件的定义就是，用户对于一件感兴趣的东西，进行的触发事件，例如一个对象，被滚动，点击，数值改变等等，这些操作动作，都可以被称作为事件

总的来说，事件就是给我们的用户提供一个接口，来给我们的用户，进行交互的，当用户进行事件触发的时候，我们就可以进行相对应的操作

那么如何为对象添加事件呢？

lv_obj_add_event_cb(obj, event_cb, event_code, user_data);

lv_event_send(obj, event_cb, event_code, user_data);

lv_obj_remove_event_cb(obj, event_cb);

lv_obj_remove_event_dsc(obj, event_dsc);    //event_dsc 是 lv_obj_add_event_cb 返回的指针

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjRlYTVjNzNkODZmYzhlY2JiNzIzYTUwYTUwNjY3NGVfSk4xTHhuR29Wd1pVNjA5NGc5aVJUb3VXYUs2S09aRlFfVG9rZW46TklPQWI3RGYyb09Ic0N4UlVrZ2NqTkxjbmtjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 函数讲解

**一、参数说明**

1. 参数一：要绑定的对象。
2. 参数二：事件处理的函数（回调函数 callback），当绑定对象的事件被触发时，执行此函数进行处理。
3. 参数三：事件代码（code），可指定特定情况或所有情况触发。
4. 参数四：用户传入的数据（user_data），在回调函数中可使用该数据满足不同场景需求。

**二、整体流程**

当对象事件被触发后，根据事件代码决定是否执行回调函数。若触发且满足条件，进入回调函数处理，可使用参数四的用户数据进行特定操作。

### 事件类型

http://lvgl.100ask.net/8.1/overview/event.html#event-codes

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTc5Y2JhMGRmYjcyZjc0ODg2YmVhZjlkZjE1NjI5NTZfS1J1UVlRZEM3WTF6UVpTSHVVUTBxeVBYcHlsU1pkc0hfVG9rZW46UENTaGJlTnllbzY0Z1h4bXpkV2NDV1o4bmZjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 源码讲解 回调函数

事件回调函数只有一个参数，这个参数对我们的作为非常大，现在的版本提供这些功能：

static void my_event_cb(lv_event_t * event);

#### 获取触发的事件代码：                    lv_event_code_t code = lv_event_get_code(e);

#### 获取触发事件的对象：                    lv_obj_t * target = lv_event_get_target(e);

#### 获取最初触发事件的对象(事件冒泡): lv_obj_t * target = lv_event_get_current_target(e);

获取事件传递的用户数据：              lv_event_get_user_data(e); 获取使用 lv_obj_add_event_cb 传递的用户数据                                                lv_event_get_param(e); 获取使用 lv_event_send 传递的用户数据

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YmY2ZWRmNmJlYzU4OWY0YTA1OTZlNjI3MTRlN2U2OTdfREw2MURiWTlxYnozOTdNTzBtdHp2RWdiNWRyZm5WM2NfVG9rZW46VXJQS2JaSERRb3VnUm14ckpTRmNHM2lKbkdkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Yzk2ODAyZmY5ZTZmZjY1ZjI5YTZkNDU1OTJiNTJiZjlfMGExQUZFS3NPc0Z1RWptQXJjNkdJdjZ3bUV1SDk4M29fVG9rZW46QTlqTWJEYXZib2hveEh4bFpoTmMySUhlbkVjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

其实我们这里的函数，他是可以传入参数的，我们转到lv_obj_add_event_cb就可以看到

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OWY1ZTI4MTAxNDliN2VjNDJiZmVhN2IzZGVlOGIxMTFfUEZteGdWcmgwaU43eHdzeVpPQ2pJMlBYc0xmSEZVNktfVG9rZW46TTZKUmJva3Fsb3NpS3J4eGZqYmNNck9PbldmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

这个回调函数里面接收了一个结构体的参数

```C++
// 定义一个名为 my_event_cb 的静态函数，接收一个 lv_event_t 类型的指针参数
static void my_event_cb(lv_event_t * e)
{
    // 获取触发事件的对象
    lv_obj_t * obj = lv_event_get_target(e);
    lv_obj_set_style_bg_color(obj,lv_color_hex(0x000000),0);
    printf("test\n");
}

void lv_100ask_demo_course_2_2_6(void)
{
    // 创建一个对象，以当前活动屏幕（lv_scr_act）作为父级对象
    lv_obj_t * obj = lv_obj_create(lv_scr_act());
    // 为创建的对象添加事件回调函数，当该对象被点击（LV_EVENT_CLICKED）时，调用 my_event_cb 函数
    lv_obj_add_event_cb(obj,my_event_cb,LV_EVENT_CLICKED,NULL);
}
```

如果想要接收所有触发方式，就要在回调函数里面进行判断，对于不同事件触发，进行不同的处理，否则，所有事件都会被作为回调函数的触发事件

```C++
 // 事件回调函数，根据不同事件代码设置对象背景颜色并打印信息
static void my_event_cb(lv_event_t * e)
{
    lv_obj_t * obj = lv_event_get_target(e); //获取结构体中的样式
    lv_event_code_t code = lv_event_get_code(e); //获取结构体中的事件代码
    switch(code)
    {
    case LV_EVENT_CLICKED: //点击
        lv_obj_set_style_bg_color(obj,lv_color_hex(0xeceec),0);
        printf("test\n");
        break;
    case LV_EVENT_LONG_PRESSED_REPEAT: //长按
        lv_obj_set_style_bg_color(obj,lv_color_hex(0x000000),0);
        printf("Helloword\n");
        break;
    default: //默认状态处理
        break;
    }
}

void lv_100ask_demo_course_2_2_6(void)
{
    // 创建对象以当前活动屏幕为父级
    lv_obj_t * obj = lv_obj_create(lv_scr_act());
    // 为对象添加事件回调函数，处理所有类型事件
    lv_obj_add_event_cb(obj,my_event_cb,LV_EVENT_ALL,NULL);
}
```

讲完前面的参数，那么最后的user data 怎么用呢

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDhmZjRmYWQ2MDNjNTM5NWIwODcwMTYzZGZkZGViZjJfZWxtM1hsNHl6YWFFZWJ3dkp5YjFuY01hYVlYemdSZnhfVG9rZW46U1ZOR2JCM2Vyb3U3ZjR4MmxXRGNFZ29jbkhoXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

可以看到这里的user data 是跟 lv_obj_t 类似的，所以我们还是通过下面的代码，来进行user_data 的获取

```C++
lv_obj_t * label = lv_event_get_user_data(e);
```

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmMwNmE0YjA2MWNjMGM2YTE2MzNhNzllMjk5NmI3ZjlfS3l3SUViOThEV3h2a2JVWWpuWXhjV2swNUloUTk0bTFfVG9rZW46Sm56SGJWaEZhb2NMbmR4MXI3MGNweldvbndoXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 事件冒泡

事件冒泡是一种事件传播机制，事件在对象上发生时会向上传播到父级对象。

在`lv_event_send(obj, event_cb, event_code, user_data)`中，

`obj`是目标对象，

`event_cb`是处理特定事件的回调函数，

`event_code`标识事件类型，

`user_data`是自定义数据。发送事件可手动触发事件并传给指定对象，如按钮按下可将事件传给另一个对象。实现方法是为按钮设置回调函数，按下时调用`lv_event_send`，再为目标对象设置回调函数处理接收的事件，以实现对象间接交互，增强程序灵活性和可扩展性。

简单介绍

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWZhNTg0NGYyZjEwODg1ZWZkZjU1ZDQ0ZjkxZGVhYWNfRGxJNmV1anpJUjBIRE9xY0pYM1BNbEU3SkpuYTJ3RHRfVG9rZW46S09mSWJrU3NXb3ZTQXN4ZXpCQmNFeGZUbmpjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

lv_event_get_target(e); 获取触发事件的当前对象。

lv_event_get_current_target(e); 获取事件冒泡的父对象。

lv_obj_add_flag(obj, LV_OBJ_FLAG_EVENT_BUBBLE)添加冒泡标志位

### 源码讲解

```C++
void lv_100ask_demo_course_2_2_6(void)
{
    lv_obj_t * obj1 = lv_obj_create(lv_scr_act());//创建对象以屏幕为父级，通过lv_scr_act进行指定
    lv_obj_t * obj2 = lv_obj_create(obj1);
    lv_obj_add_flag(obj2, LV_OBJ_FLAG_EVENT_BUBBLE);//开启obj2对象的事件冒泡


    lv_obj_t * label = lv_label_create(lv_scr_act());
    lv_label_set_text(label,"test");
    lv_obj_center(label);

//添加回调事件，要发生事件的对象为obj1,回调函数，触发方式，用户数据
    lv_obj_add_event_cb(obj1,my_event_cb,LV_EVENT_ALL,label);
}
```

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODc2NjRhZjkyMzVmNjFkZjA2MTA2OTQ0OTcxZWZlYjhfZXlyeGNWeEpLSVdRNnNQdFhHMkE5ak80dWxsUlBib2NfVG9rZW46UzA2cmJkT2pib1d0dEl4dDlpTGN6dVFDbjRiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

首先这里已经获取了，当前触发事件的对象，那么我想要找到最终获取的对象怎么操作呢

```C++
typedef struct _lv_event_t {
    struct _lv_obj_t * target;
    struct _lv_obj_t * current_target;
```

在 `lv_event_t` 结构中，`target` 和 `current_target` 有以下区别：

`target` 表示触发事件的原始对象，即事件最初发生在这个对象上。

`current_target` 表示当前正在处理事件的对象。在事件冒泡的过程中，这个值可能会随着事件在对象层次结构中向上传播而改变。如果没有事件冒泡，那么 `current_target` 和 `target` 通常是相同的。

### 总结 

开启对象的冒泡之后，target 的 trigger event 就会传入到 current target

暂时无法在飞书文档外展示此内容

并且一个事件的回调函数可以给多个对象使用，就比如我们这里的callback里面的对象是只有obj1 的，但是多个对象的冒泡都传递到了obj1里面，这样就是一个回调函数可以给多个对象使用

一个对象可以使用多个事件回调函数，这也并不难理解

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODU2YjllYWI1YTdkYTNlOTZhNTA0MmIxZWQwNDc4NzJfTGZnMURFemh0MzJVZEdaUE1RZE85QkQ0ZlhOV1FXZFZfVG9rZW46RnVmZWJGcEg4b3N2MGV4ck1mamMyekwzbkZjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

其他的例子

```C++
    lv_obj_t * label = lv_label_create(lv_scr_act());
    lv_label_set_text(label,"test");
      lv_obj_t * labe2 = lv_label_create(lv_scr_act());
    lv_label_set_text(labe2,"label");
    lv_obj_align_to(label,obj1,LV_ALIGN_OUT_TOP_MID,0,0);
    lv_obj_align_to(labe2,obj1,LV_ALIGN_OUT_BOTTOM_MID,0,0);

    lv_obj_add_event_cb(obj1,my_event_cb,LV_EVENT_ALL,label);
    lv_obj_add_event_cb(obj1,my_event_cb,LV_EVENT_ALL,labe2);
```

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OGM3MGU0NTViYjgwZTliOGUzNjhhZmU0NGY3YjA1NDhfU21jaHo0SFFaNkNvMDRrS3ZROUZWSHNPSnJsTFlXUHhfVG9rZW46VVYzVmI4S2F1bzhzUGR4bU5qQ2NQRXFlbmJGXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

# 文本标签

前面有提到过，我们的对象呢，就可以看作为一个盒子，那么这个标签

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTNkY2MyZGQxOGM2Y2VjMmRjNzMyOWViNTY4MjdiZjdfYlg4QlM3MWlsUTdmSmcxTnJINVQyWVZ3TXlIZWt0VktfVG9rZW46RXpJcmJHa2Zab0M5YmJ4RnRWVGM1TlBDblRnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 设置显示文本

直接显示:lv_label_set_text(label, "New text");

格式化显示：lv_label_set_text_fmt(label, “%s: %d”, “Value”, 15);

文本存储在缓存区中：        lv_label_set_text_static(label, "New text");

文本换行lv_label_set_text(label, " line1\nline2\nline4 ");

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MGU5NDIzYzBlOGEzODAwN2YyOTdiZjgzMDgyMWE1NzZfQzBhSTZxY2xiZ3V6Y1cxT29WNXB5MnVsWFlYRmhlU1VfVG9rZW46TW1mNWJ0MnpjbzJsM0N4Um5oVWNkNkJwbnBmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

这里我们可以看到，不论我们的文本怎么增长，换行，标签都可以自适应，其实除了这种模式，标签还有其他模式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWI0MWNmODczMGFmMmViYmEwZTE5NzQ0MTRmMjEzZTJfQWdIMTNXQU5nSlVjZUszNWt0VGtJdTJobkxXVFNmaHRfVG9rZW46RmwzYWJVZWJjb2J3WWt4d2d2ZGNObVNHblJkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 大小

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OWUwZTQxYjJmNzEwMGMxYmJiYjgwNWNjY2JlNmY5MjhfS29sOHZ6RmkyQzhxVWtVdU5UMmdWM093UmVPTXUyREZfVG9rZW46VFBoQ2JKWkczbzRuVXJ4WUdkVWNGcHY5bjJTXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 显示模式

如果我们指定他的大小就会出现显示不全的情况

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjVhYTg0MmE0ZGQwZjc3ZTIzOTJmMjg2ZDZmMWJiZjhfSDJab3BVTmc1N2g0ekdkVW52dkIxaTVRQ1AzSTFJTGRfVG9rZW46VTY2SWI5bUdnb3JKcWh4a2RxY2NaRmN6bnZoXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NThjNDU2YjM3NjVhMzIwMmRiM2U3OTc3NGQwM2Y4Y2ZfeXA3SlVxZHVjSjBIcUNKanROdlRCNnRvMllOOFVVZXZfVG9rZW46VzVvQmI0RWh5b2ZKVVV4WTVwNmN0RFRWbkVnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

####  lv_label_set_long_mode(label, LV_LABEL_LONG_...) 

通过这个函数就可以进行模式指定

LV_LABEL_LONG_WRAP 默认设置自动适应

LV_LABEL_LONG_DOT 如果文本太长，就保持大小并在末尾写3个点 .

LV_LABEL_LONG_SCROLL 如果文本比标签宽(太长)，则可以水平来回滚动显示它。

LV_LABEL_LONG_SCROLL_CIRCULAR 如果文本比标签宽，则水平滚动它。

LV_LABEL_LONG_CLIP 剪掉超出标签范围外的文本部分。

#### 注意⚠️

#### 如果使用 lv_label_set_text_static，因为它是静态内存，只读不可写，所以在一些需要修改文本缓冲区的操作中可能会出现问题。而动态内存分配的情况下，代码可以在新开辟的区域进行修改，就不会有这样的问题。😃

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MWU2MzI4MGY3OTViMTJjODFhYjc0ZTU1NzgxZTY1NjFfY1BQeURJcFhlVzhndGpwRzBOZ2s3YXo5NHZhbEg5alRfVG9rZW46VlRDOWIxWGZPb3VSdWJ4Uk5VR2MxSjRLbmFiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

具体可以见到下图

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzZkZDg1YWZlOWIwMWM3Y2EyNmIyMzg5NzlhNzNiYmVfZHNXY1FKanBJZkxXdXlVVWhuNXFwcnFKQ2dtNEl3NGdfVG9rZW46REcyRmJRank4b0dRQTF4NjFZa2NHOEkxblNnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 文本着色

这里改变文本的颜色，可以通过共享样式跟本地样式进行改变

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZGI5NTQ5NDNhOWJkZWQ0NTY4Y2NiMmVkNWNlMDhmZjhfV0kzclduZGZ3dGpBVnVGdXVsSVRRZTZ3emFTV25tRUhfVG9rZW46Q3B2SmJuZ3hSbzhGcXp4eVE5WmNUcWw0bjNlXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

这里我们再复习一下本地样式跟共享样式的区别

1.在 LVGL 中，共享样式可被多个对象共用，能提高内存使用效率，减少重复定义，一旦修改，所有使用该共享样式的对象都会受影响；

2.而本地样式是专门为特定对象定义，只对该对象起作用。并且本地样式的优先级高于共享样式，当两者对同一属性有不同设置时，本地样式会覆盖共享样式。

### 例子

#### 设置透明度

这里的背景透明度默认数值为0 ，我们要想让他显示东西，就需要对透明度进行设置

```C++
lv_obj_set_style_text_color(label, lv_color_hex(0xf7b37b), 0);//文本着色

lv_obj_set_style_bg_color(label, lv_color_hex(0xf7b37b), 0);
lv_obj_set_style_bg_opa(label, 100, 0);
```

#### 重新着色

这里仔细看不难发现，前面跟上16进制的颜色以后，后面再跟上想要上色的字符串，期间用##进行区分

```C++
也可以让文本某些部分重新着色，例如：       
 lv_label_set_recolor(label1, true);        
 lv_label_set_text(label1, "#0000ff Re-color# #ff00ff words# #ff0000 of a# label);
```

#### 文本选择

在“lv_conf.h”中开启“LV_LABEL_TEXT_SELECTION”（默认开启）后，可以选择部分文本，此效果在 PC 上类似用鼠标选中文本，**但仅能在文本框“lv_textarea”中自动实现**。对于“Label”，需手动选择指定范围文本，通过“lv_label_set_text_sel_start(label, 1)”

“lv_label_set_text_sel_end(label, 6)”

### 内置图标

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NjA1NDVkYjc4N2I3ZmUwOWUzMWI1OGMwNmNmZWQ4ZDVfZlRCVjh0YktieEw1MzZpMnBxUzNRaWJTMGJvcHJMQmlfVG9rZW46WWtsQ2JjTkg0b3BENXZ4c2pKcmNNM244bkNiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

lv_label_set_text(my_label, LV_SYMBOL_OK);        // 直接显示图标      

lv_label_set_text(my_label, LV_SYMBOL_OK “Apply”);         // 图标与字符串一起使用        lv_label_set_text(my_label, LV_SYMBOL_OK LV_SYMBOL_WIFI LV_SYMBOL_PLAY);         // 多个图标一起使用

### 事件处理

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Zjg4NzYwYjYzOTcwYjRkZDJhNWQwYzJjNjgyOGZmMmJfUEVHVTZYN0NxZnBwVHhuM3lPMHdFOWR4MGtmSTFpYklfVG9rZW46UWpzSmJza0Fjb1JtbjZ4OEdmcWMweU5Kbm5jXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

 lv_obj_add_flag(label, LV_OBJ_FLAG_CLICKABLE);  // 使输入设备可点击对象

### 字号调整

这里的字体可以看到，默认都是14号字体

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YWEzMzc0NTEzNjZjNmE5ZDFhNzFkMmJkNDFkYjViMTBfMkZkeFBTUUs5RHA4NDBRR2RXaHNBMm5OTmQyZ05FR1pfVG9rZW46TTNmSWJOd0tNb0VMU2h4YWNISWNXdEJlbkxiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 中文显示

Src的意思就是source 源头，用于存放源代码，那么这里面有很多lvgl 自带的字体样式，其中也包括了中文字体

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTY3MDVjYTRkZWNjOTNhMGM3Y2Q5NjI2Y2U2Yzk2MDhfMzRJbXExQjV5dXQybXRJRjc0bVdQekx4dEtxbnhKTGZfVG9rZW46VUIwbWJTeHVGb2xWNXB4YUZXUGMweWpTblBiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

注意这里需要显示中文的话，编码格式必须要改成utf-8 否则默认的windows-936是无法显示内容的

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTk0MDIzMjhkMzIxOGJlNjU0YmIyZjE4MGNiOGM0ZDlfS0ZYbkZzaXdNM01ZS0M4Y0JmMmVJR1hiZEM0ZEhtMmRfVG9rZW46R3ZhMGJodTdPb0JXYTZ4TzZTb2MyT1VPbmlnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 取模

那么通过字体文件跟字体转换器，我们就可以进行过获取

LVGL内置有一个中文字库 CJK字库 ，这个字库在 lv_conf.h中定义为：LV_FONT_SIMSUN_16_CJK。

要在lvgl中使用显示自己的中文字库，我们需要用到两个东西：字体文件和字体转换器。

字体文件我们可以使用开源的字体或者自己制作出来，准备好了字体文件之后使用字体转换器即可转换成可以在lvgl上使用的字体格式。开源字体获取页面：        http://lvgl.100ask.net/8.1/tools/fonts-zh-source.html

准备好字体文件之后就可以通过lvgl官方提供的字体转换器，提取转换你想要的字体，LVGL官方在线字体转换器页面：       https://lvgl.io/tools/fontconverter

### 字体转换器

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTk1NWE5N2Y2MjIwZGE1MDE0YWRjNGQzOGFhM2YwYTJfZ0NEdzF0REpPQU9JODRaVmpyRnVnb003aEdkUWhUbXZfVG9rZW46V08zcGJ3V2cwb2Nnbzl4aHV5emNFRkNvbk5kXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MDFiOThjMTJkZDlmZmRmMTU5NmI4MGE5N2Q3NzE0ZjlfZ2JQWjdmV3BrRUZNdldCWWFwUXQydXNpaVdyMVllbGlfVG9rZW46SFA1WGI0STF1b2JxTDl4c0RYRmNKZFdIbjNkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=OTIxMTBkOWU0NzNmYzQ5ZDUzNTNlNmZiMzM0YWNlNTFfZFliM3huM09kYjhvejA4RXdVYThmbVg2SURDSHZndTVfVG9rZW46VzZsOWJHYnpob2ZUNmV4YWR5dmNWM2JCblFjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 按钮

按钮其实跟基础对象非常类似，但是他有最重要的一点，就是可以添加到默认组里面，可以修改为其他输入设备进行控制

### 创建按键的方法：         lv_obj_t * btn = lv_btn_create(parent);

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=Njk0NTc0MTFjZDdhNWRmMjkxYjExY2E5MGRmNDViNDNfd1ROdm9QaExIcWNmM3RkRFo4RWo0SVROem1jU1ZCNWJfVG9rZW46Qm10T2JEYjN1b3plU3N4R1JjZWNlallIbnNmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

### 部分和样式

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NDE3MGQ2YTAwOTI0YTI0YTVhZjQyZjczMWE4NzM5NzVfaWRpVktQck5nNlhxZ3NzUTBpSER5NXJTRHBzREJDcU1fVG9rZW46Sm40RmJ5OWxqb3VEN1R4QkhxVmNMMGF4bmNmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

样式修改示例：        

lv_obj_set_style_<property_name>(obj, <value>, <selector>);        // 本地(私有)样式        lv_obj_add_style(obj, &style, <selector>)                        // 普通(共享)样式所以修改样式的时候我们修改部分(Part)的时候只有 LV_PART_MAIN 可以生效；状态部分和前面说的样式状态(States)都可以

### 源码讲解

这里的两种属性是可以组合使用的，当按键被按下的手，才会进行颜色的更改

```C++
 void lv_100ask_demo_course_3_2_1(void)
{
    /* 创建一个btn部件(对象) */
    lv_obj_t * btn = lv_btn_create(lv_scr_act());       // 创建一个btn部件(对象),他的父对象是活动屏幕对象

    //修改样式
    lv_obj_set_style_bg_color(btn, lv_color_hex(0xf0d0e),LV_PART_MAIN  | LV_STATE_PRESSED);
}
```

## 探讨

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YWE3OWI5NGI5ODMwZmExZGEwNDFhMWM3YzNjNjIzNDZfTTYwTWFOeHV2MFNnYlFXSmcxWmN4NnlBUEIwWjA3THRfVG9rZW46QUhKdmJKZlBMb2s5dnJ4VXVKWGNDanJhbjNlXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

# 物理按键代替触摸

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NTgwYTcxMGUwMjUxNjkzYzkwZjE1MDU0MjUwODZkYzFfbkpoOTJYY3hTWUpQMDhQdFI0eU5YeE5SQ3FCenNXOW1fVG9rZW46RGR5TGJOS2M4b2JIRTR4bTZ4UGNvQm5lbktjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 组

这里我们引入一个概念，在lvgl 中，他把一个个需要通过物理按键控制的对象放在组里面进行管理，然后这个组呢，就会通过我们的输入设备，比如键盘，获取到键值，然后发送到组里面，组再进行相对应的处理，那么这里呢就有三个步骤了

暂时无法在飞书文档外展示此内容

### 自定义组创建过程

在使用 LVGL 时，首先需要创建一个组（Groups），即通过 

`lv_group_t * g = lv_group_create();` 创建组对象。接着，将一个对象添加到这个组中，使用 `lv_group_add_obj(g, obj);`。最后，要将组与输入设备相关联，

其中 `indev` 是 `lv_indev_drv_register();` 的返回值，通过 `lv_indev_set_group(indev, g);` 来实现关联

放在代码上就是这样的效果了

```C++
    lv_group_t * g = lv_group_create();//创建一个组
    
        /* 创建一个btn部件(对象) */
    lv_obj_t * btn1 = lv_btn_create(lv_scr_act());       // 创建一个btn部件(对象),他的父对象是活动屏幕对象
    lv_obj_set_size(btn1, 100, 50);
    lv_obj_align(btn1, LV_ALIGN_CENTER, 0, -100); 
    
    
    lv_group_add_obj(g,btn1); //将对象添加到组内
```

但是一般情况下，我们会直接在创建的时候，就将对象添加到组中，也就是将对象添加在默认组中

lv_obj_t * btn2 = lv_btn_create(lv_scr_act());

## 按键控制的初始化、工作流程和使用

这里可以看到，对于组初始化的底层，就是初始化了一个链表，我们把我们的部件添加到了组里面，其实就是放在我们的链表里面，这个组里面

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ODVjOTFiMGRmMGMyOGRhY2M4MjU2YjY2ZDI0MmVkNTFfZkZqNThYNmlzTE50VkFVcXJmdEVJcm0wYVZLRnRHT1ZfVG9rZW46SGU3d2JkY0tGb0hCd254R1NWWmMxSXVubnpkXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YTJmNzUzZTlmZmY0ZjhlY2YzY2VhYWNiYjkwMzMwMDJfa3BFS3ZKZDNQMThKRjl3UFphMDlCNzZ3V3dDSTY1OWVfVG9rZW46WExISWJ2VmFobzRkV054TTRXRWNrSzl1blBnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

实体按键移植的时候，要重点关注这一部分，其中这里的lv_indev_state_t 是获取到按键的状态，将它赋值给data 中的state 成员 然后判断按键是按下还是抬起

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDk5YTJmOTVhZmVhOWQ1MGIzOTllMzgzYWE5NzRjY2JfU284eW9SazAwZ3J6Q2VxSjBsbWVzcDlVeFJhSmdhUUhfVG9rZW46QUtXdGJqeTd6b0FCTnp4RU9SSGNMWW52bm9jXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

```C++
static void lv_win32_keypad_driver_read_callback(
    lv_indev_drv_t* indev_drv,
    lv_indev_data_t* data)
{
    // 忽略输入设备驱动参数，这里只是占位，表明不使用该参数
    UNREFERENCED_PARAMETER(indev_drv);

    // 根据全局变量 g_keyboard_pressed 的值设置输入设备的状态
    // 如果 g_keyboard_pressed 为真（键盘被按下），设置状态为 LV_INDEV_STATE_PR（按下状态）
    // 如果 g_keyboard_pressed 为假（键盘未被按下），设置状态为 LV_INDEV_STATE_REL（释放状态）
    data->state = (lv_indev_state_t)(
        g_keyboard_pressed? LV_INDEV_STATE_PR : LV_INDEV_STATE_REL);

    // 获取全局变量 g_keyboard_value 的值，并赋值给局部变量 KeyboardValue
    WPARAM KeyboardValue = g_keyboard_value;
}
```

暂时无法在飞书文档外展示此内容

基础对象的作用

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=NmQ5OWU5YjgwNGNlOTJiMTk4Yjc4ODFiYmRiOTc3MDRfMTZyZzNlVDVXdGUwQkhUc1VTYlhlVG5rVm9qNlMwT1hfVG9rZW46QlBkbmJEYnMwb1ZGZ2F4WE45RWNpUFIxbjZiXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

那么对象如何知道自己被聚焦，并且做出回应的呢？，这里的定位思路就是

这里的所有对象，都被创建在屏幕这个父级上面，而屏幕的创建又被分成了三级

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=YzMzNWYzODg2MWQwY2U1NWJiOGU4OWI2NTVkMzA2YmRfZzNIdXBab0pwbFdid244T3ZLUzVISHFVRTlYdWd6SjhfVG9rZW46SkIzMmJZSUF6b2F2bTd4WlNZS2NMajJabjlmXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

分别是活动层，顶层，与系统层

### 特批记录

今天终于学会了，实体按键移植，应该算学会吧哈哈，回头再看之前教程的代码，不再是一窍不通，这种感觉让我很欣喜特此记录一下 2024年11月13日17:00:48

## 代码讲解

```C++
    // 初始化输入设备
lv_port_indev_init();

// 创建一个输入设备组
lv_group_t *group = lv_group_create();

// 将名为'indev_keypad'的输入设备设置为属于刚刚创建的输入设备组
lv_indev_set_group(indev_keypad, group);
```

# 开关（lv_switch）

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjkyNDliMjkwMzczNDRjYTllOWM0ZTVkOGIyYTgyMjhfRUNFMW1oMzVSMHVqTUV4dVNzRU02VnNEUnFnQnAyU1RfVG9rZW46TnlEU2JLWEVYb3VLZnN4TjE5RmM0OVpmbkJnXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 零件和样式

**一、背景相关（LV_PART_MAIN）**

1. `lv_obj_set_style_bg_color(sw, lv_color_hex(0xc43e1c), LV_PART_MAIN)`：用于设置开关背景颜色
2. `lv_obj_set_style_pad_left(sw, 5, LV_PART_MAIN)`：用于设置背景左边的填充值

**二、指示器相关（LV_PART_INDICATOR）**

1. `lv_obj_set_style_bg_opa(sw, 100, LV_PART_INDICATOR)`：用于设置指示器关闭状态背景不透明度
2. `lv_obj_set_style_bg_color(sw, lv_color_hex(0xc43e1c), LV_PART_INDICATOR)`：用于设置指示器关闭状态背景颜色
3. `lv_obj_set_style_bg_color(sw, lv_color_hex(0x7719aa), LV_PART_INDICATOR | LV_STATE_CHECKED)`：用于设置指示器打开状态背景颜色

**三、旋钮相关（LV_PART_KNOB）**

1. `lv_obj_set_style_bg_color(sw, lv_color_hex(0xc43e1c), LV_PART_KNOB)`：用于设置旋钮颜色，可标号为 “KNOB_COLOR_SET”。

这里再提到一个方法就是 样式 | 触发条件，这样就可以通过触发条件去改变样式

## 用法

**一、获取开关状态**

当开关被打开的时候，开关的状态就会变成为 LV_STATE_CHECKED我们可以通过下面两个接口获取开关的状态

- `lv_obj_has_state(switch, LV_STATE_CHECKED)`：返回 bool 类型表示开关是否处于打开状态。
- `lv_obj_get_state(switch)`：返回枚举类型开关状态。
- `lv_obj_get_state(switch)`：返回枚举类型开关状态。

**二、设置开关状态**

一般我们通过输入设备对开关进行设置，其实我们可以手动控制开关打开跟关闭

- `lv_obj_add_state(switch, LV_STATE_CHECKED)`：设置开关状态为checked。
- `lv_obj_clear_state(switch, LV_STATE_CHECKED)`：关闭开关。

**三、设置开关不可更改状态**

通过以下接口对按钮设置不可更改状态

- `lv_obj_add_state(sw, LV_STATE_DISABLED)`：添加按键状态为失能
- `lv_obj_add_state(sw, LV_STATE_CHECKED | LV_STATE_DISABLED)`：开启按键并且添加按键为失能

**四、恢复开关可更改状态**

- `lv_obj_clear_state(switch, LV_STATE_DISABLED)`：清除失能状态正常使用

## 事件处理

正常情况下，当开关被点击并且状态发生改变时，会触发 LV_EVENT_VALUE_CHANGED 事件类型。也就是说我们可以在 LV_EVENT_VALUE_CHANGED 事件类型中处理事件

比如：lv_obj_add_event_cb(switch, event_handler, LV_EVENT_VALUE_CHANGED, NULL);一样的

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=MTA3ZDljYWNiNmM3Mjk2YWMxZGQ2YjYyMDc4YWEzMDdfbHNkWkRUZnVkS004Rkc2MTVHa0dybmpqRFBvWW5FSEZfVG9rZW46V0xadWJ5R3lEb0M0a0V4SEZwUmM0OXZ4bmNzXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

然后复习一下这里的lv_event * e 这个参数，通过lv_obj_add_event_cb ——> lv_event_t 就可以知道

## 源码示例

```C++
//通过bool类型，判断开关状态，并打印输出

 static void my_event(lv_event_t * e)
 {

     lv_event_code_t code = lv_event_get_code(e);
     lv_obj_t * sw = lv_event_get_target(e);

    if(code == LV_EVENT_VALUE_CHANGED)
    {
    if(lv_obj_has_state(sw, LV_STATE_CHECKED))
        LV_LOG_USER("ON!");
    else LV_LOG_USER("OFF!");
    //lv_obj_get_state(sw);//返回枚举类型开关状态。

    }
 }
```

这里将开关也放在组里面，然后将输入设备替换成编码器，这样就可以通过鼠标的滚轮，进行控制了

这里再复习一下，实体按键移植的流程，首先创建一个组，那么对象默认都是添加在这个组里面的，然后将组与输入设备进行捆绑，最后将物理按键输入数值传入输入设备

```C++
    lv_group_t * g = lv_group_create();//创建一个组

    lv_group_set_default(g);//将g组设置为默认组

    lv_indev_set_group(lv_win32_encoder_device_object,g); //设置组的索引为编码器
```

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDhmZTFmMjI0ZDJiNGQ2ZmVkNDU2ODc2ZjE5N2Q2ZTJfQ1NWTUNyTlliQnd4bXRRN2xhbFRYbE5ndGFCZFB2cVdfVG9rZW46T3pva2JMOVBUb1lyYXd4c3dkdWMzVUwwbkNwXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

## 复选框

复选框(checkbox)由“勾选框”和标签(label)两部分组成，复选框的功能类似于按钮，也可以用来打开和关闭(触发)某些东西。

创建复选框的方法：        lv_obj_t * cb = lv_checkbox_create(parent);

### 零件和样式

只要是对象， 就离不开零件与样式其中，复选框包含了三个零件 背景、勾选框与文本之间的间距 以及勾选框的大小

![img](https://xcn3vp30kv5p.feishu.cn/space/api/box/stream/download/asynccode/?code=ZDIyYzNlMzI3NGVjNGMxZWYwOTI4MWNkODJiYzc3ZWFfZEZRVUdXcEZJZVJDZk1RcDFNMklMa0NqbGk3akFZZVpfVG9rZW46S0JUeGJ4TTVyb3dVZDl4cUpWeGNFRGcybktjXzE3NDE0MzI4MzI6MTc0MTQzNjQzMl9WNA)

首当其冲的就是背景颜色

以下是对复选框相关内容的分类总结：

**一、组成零件**

1. `LV_PART_MAIN`：
   1. 作用：代表复选框的背景。
   2. 相关函数：
      - `lv_obj_set_style_bg_opa(cb, 100, LV_PART_MAIN)`：设置背景不透明度。
      - `lv_obj_set_style_bg_color(cb, lv_color_hex(0xc43e1c), LV_PART_MAIN)`：设置背景颜色。
      - `lv_obj_set_style_pad_column(cb, 100, LV_PART_MAIN)`：调整勾选框和标签之间的间距。
2. `LV_PART_INDICATOR`：
   1. 作用：代表复选框的勾选框部分。
   2. 相关函数：
      - `lv_obj_set_style_bg_color(cb, lv_color_hex(0xc43e1c), LV_PART_INDICATOR)`：设置勾选框勾选时的背景颜色。
      - `lv_obj_set_style_bg_color(cb, lv_color_hex(0x7719aa), LV_PART_INDICATOR | LV_STATE_CHECKED)`：设置勾选框不勾选时的背景颜色。

### 用法

**一、获取复选框状态**

1. `lv_obj_has_state(cb, LV_STATE_CHECKED)`：返回布尔类型，用于判断复选框是否被选中，开为 1，关为 2。
2. `lv_obj_get_state(cb)`：返回枚举类型，可获取复选框的具体状态，如 LV_STATE_...。

**二、主动设置复选框状态**

1. `lv_obj_add_state(cb, LV_STATE_CHECKED)`：主动勾选复选框。
2. `lv_obj_clear_state(cb, LV_STATE_CHECKED)`：主动取消勾选复选框。

**三、设置复选框不可更改状态**

1. `lv_obj_add_state(cb, LV_STATE_DISABLED)`：设置当前未勾选状态的复选框不可更改。
2. `lv_obj_add_state(cb, LV_STATE_CHECKED | LV_STATE_DISABLED)`：设置当前已勾选状态的复选框不可更改。

**四、恢复复选框可更改状态**

`lv_obj_clear_state(switch, LV_STATE_DISABLED)`：清除禁用状态，使复选框恢复可正常使用状态。

### 事件处理

正常情况下，当复选框被点击并且状态发生改变时，会触发 LV_EVENT_VALUE_CHANGED 事件类型。也就是说我们可以在 LV_EVENT_VALUE_CHANGED 事件类型中处理事件，

比如：         lv_obj_add_event_cb(cb, event_handler, LV_EVENT_VALUE_CHANGED, NULL);