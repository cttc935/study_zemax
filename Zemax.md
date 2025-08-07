# Zemax

## 点阵图

1. 快速查看系统的成像质量，在大像差的情况下比较直观

![image-20250716145248317](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716145248317.png)

  设置了六个视场，这里就有六个点阵图，在图像上方显示的对应的视场，下方的像面数据就是对应的像高，**右上角不同颜色对应不同的波长的光线**

由图可知，红色弥散斑很小，蓝色大，蓝色的色差大

最下方会给出具体的数值

**RMS**均方根半径：能力集中程度（评价质量）

**GEO**几何最大

2. 系统的像差比较小的时候点阵图的值比较小，小到一定的程度点阵图就不再适用

点击上方的设置，显示艾里斑Airy disk

![image-20250716150304557](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716150304557.png)

![image-20250716150501077](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716150501077.png)

在视场的上方显示的艾里斑半径，**现在这个情况艾里斑半径远小于弥散斑的直径**因此可以用点阵图来评价成像质量

当艾里斑半径大于或者接近弥散斑 **点阵图已经不适用了**

## MFT光学传递函数

### 像差小于一定的值光学传递函数才有意义

![image-20250716150809340](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716150809340.png)

**在频率很低的时候就几乎等于0，说明像差非常大！**

![image-20250716151134551](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716151134551.png)

可以在特定频率下查看MTF大小，通过更改最大频率处的频率来实现

## 均方根--波像差

1. 真实波前图

   ![image-20250716151533596](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716151533596.png)

   2. 均方根的波像差

      1.随视场、波长、离焦变化

      ![image-20250716151843680](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716151843680.png)

      

      ![image-20250716151743096](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716151743096.png)

      

## 场曲和畸变

1. 位置![image-20250716152031728](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716152031728.png)

   **左侧是场曲**     **右侧是畸变**(关注下面的百分比还是绝对值，在设置中的显示可以更改）

   在最下方的文本可以看数据

2. 网格畸变

   ![image-20250716152545311](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716152545311.png)

   如果有的话，会向内收缩或者向外伸展

## 光线痕迹图

非共轴的光学系统（反射式的，很有用） 

![image-20250716152706087](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716152706087.png)

在设置中可以查看不同面上的光线实际痕迹

## 垂轴像差

![image-20250716153001863](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716153001863.png)

## 光线追迹数据

![image-20250716161730376](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716161730376.png)

**![image-20250716161738723](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250716161738723.png)**

Hx和Hy代表物面坐标，Px和Py代表瞳面上的坐标

**非共轴的反射光学系统里面非常有用**

# Zemax优化

## 1.建立评价函数

![image-20250717102011051](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717102011051.png)

通常不是人工建立，一般是用程序给到的**tools**

在zemax2018版本中对应**优化导向**![image-20250717102248254](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717102248254.png)

一般优化的时候**不采用**均方根RMS，而是采用分布值**PTV**

![image-20250717102348231](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717102348231.png)

一般来说想要**（MTF）波形态比较好的话选择 wavefront 波前** 

参考一般原则上选择**主光线（chief Ray）**，光瞳面环带一般选择最大，光线越多对校正像差越有利，**臂也最大**12，臂是光轴向外辐射的光线条数，如下图

![image-20250717103347627](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717103347627.png)



点击确定后评价函数会自动生成

![image-20250717103430575](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717103430575.png)

### 评价函数的字母代表什么

* EFFL 焦距
* MNEG 最小边沿玻璃
* MNEA 空气厚度
* MNCG 最小中心玻璃
* MNCA 最小空气厚度
* MXCG 最大中心玻璃
* MXCA 最大空气厚度

![image-20250717105417386](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717105417386.png)

**面1到面3 目标 权重**

## 2. 确定自变量

所有能改变的都可以作为自变量

### 1. 半径

![image-20250717105822537](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717105822537.png)

**ctrl+z快捷键设置变量**

### 2. 玻璃

将玻璃设置为自变量，就会变成小d光的折射率，以及阿贝数

![image-20250717110439118](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717110439118.png)

但是这个玻璃可能会不存在，原则上不使用**（一般是校正后期，像差仍不满意，成像质量不到最优，可以将玻璃作为自变量来矫正）**

## 3.执行优化

位置：

![image-20250717110753633](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717110753633.png)

打开执行优化后，将自动更新打开![image-20250717111125032](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717111125032.png)

然后将自己关心的像差图打开，点列图，系统图……

![image-20250717111338176](C:\Users\17737\AppData\Roaming\Typora\typora-user-images\image-20250717111338176.png)

EFFL 焦距

WFNO 光圈数

ENPD 入瞳直径

TOTR 光学系统长度 透镜第一个表面顶点到像面的距离