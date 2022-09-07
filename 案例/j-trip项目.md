# 要点
## 跳转页面
1. router-link
![[Pasted image 20220907130703.png]]
2. router.push
![[Pasted image 20220907130616.png]]

## 返回页面
![[Pasted image 20220907132108.png]]


## 网络请求
1. seachCity. vue+sevice (jcity/jRequest) 直接获取
vue
![[Pasted image 20220907180949.png]]
```html
<!--1.直接获取 "?."(判断如果有数据再拿,刚开始的时候allCity是空数组,因此拿不到),缺点是需要清除数据里有哪些key名("cityGroup"...) -->
  <van-tab :title="allCity?.cityGroup?.title"></van-tab>

  <van-tab :title="allCity?.cityGroupOverSea?.title"></van-tab>
```
2. seachCity. vue+sevice (jcity/jRequest) 遍历
vue
![[Pasted image 20220907180949.png]]
```html
<!-- 2.遍历 .vue+service-->
  <template v-for="(value,key,index) in allCity" :key="key">
  <van-tab :title="value.title" ></van-tab>

  </template>
```

3. seachCity. vue+service (jcity/jRequest)+ stores (axiosCity-->useCityStore)
vue
![[Pasted image 20220907181347.png]]

```html
  <!-- 3.遍历 .vue+store+service -->
<template v-for="(value,key,index) in allCities" :key="key">
  <van-tab :title="value.title" ></van-tab>
  </template>
```

stores--axios
![[Pasted image 20220907181725.png]]



view-->.vue 组件显示页面 (拿数据)
stores 发送网络请求
service 具体请求的操作 (管理url)







----

# 问题:



## 能否三端都较好适应

