q:
1
![[Pasted image 20220408190800.png]]
图片居中能否不用 padding
去除间隙
![[Pasted image 20220418105846.png]]

2 这样写有什么问题
![[Pasted image 20220417191459.png]]
a:
![[Pasted image 20220417191606.png]]
顺序不能反, 下面会覆盖上面的语句

3  softmusic
![[Pasted image 20220418015357.png]]
![[Pasted image 20220418015501.png]]
空格问题

## 网易云音乐项目
![[Pasted image 20220421213113.png]]
1. 为什么没有显示
 a: background-img 不能写 position
     background 才能在精灵图后面加 position
2. 为什么竖线看着是横的
![[Pasted image 20220424021109.png]]

3. 为什么全选不上 (main-left)

![[Pasted image 20220424225401.png]]

区分
```css
    flex-grow: 0;

    /* flex: 0; */

    /* flex-shrink: 1; */
```

![[Pasted image 20220425020523.png]]

![[Pasted image 20220426162934.png]]

![[Pasted image 20220426163805.png]]

![[Pasted image 20220430113324.png]]
省略号不显示原因

height 什么情况会继承
验证 line-hight 的继承

为什么需要定位
![[Pasted image 20220428231242.png]]


放大不能对齐
![[Pasted image 20220503145551.png]]


less复用伪元素
![[Pasted image 20220507004147.png]]
![[Pasted image 20220507004006.png]]
tag 和 ticket 为同一个元素的类名