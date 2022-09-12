# 1 项目预览


![[Pasted image 20220909135508.png]]
![[Pasted image 20220910120031.png]]
# 2 home
## 2.1 要点

### 2.1.1 修改 ui 组件库的样式
1. 插槽 (插入自己的元素, 然后在自己的作用域中直接修改这个元素)
	```css
	.tab-bar {
    img {
      height: 30px;
    }
  }
	```

2. 找到对应的类名/变量名
	全局修改 ![[Pasted image 20220909210652.png]]
	局部修改 ![[Pasted image 20220909210800.png]]

3. : deep 找子组件的类 (加: deep 或去掉 scoped) ![[Pasted image 20220909210913.png]]


### 2.1.2 隐藏页面
1. v-if
router-->index. js
![[Pasted image 20220907193235.png]]
App. vue
![[Pasted image 20220907193446.png]]

2. css
```css
  .city{
    position: relative;
    z-index: 9;
    height: 100vh;
    background-color: #fff;
    overflow: auto;
  }

```

### 2.1.3 返回页面
![[Pasted image 20220907132108.png]]

### 2.1.4 跳转页面
1. router-link
![[Pasted image 20220907130703.png]]
2. router.push
![[Pasted image 20220907130616.png]]

#### 2.1.4.1 跳转页面并传递数据
2homeSearch.vue
![[Pasted image 20220909224222.png]]
5homeSearchBtn.vue
![[Pasted image 20220909224116.png]]
### 2.1.5 固定部分页面滚动
![[Pasted image 20220908163850.png]]

### 2.1.6 网络请求
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


view-->.vue 组件显示页面 (拿数据)
stores 发送网络请求
service 具体请求的操作 (管理 url)

stores-->axiosCity
![[Pasted image 20220907181725.png]]

service-->jCity
![[Pasted image 20220907181826.png]]


### 2.1.7 网络请求总结
store-->modules-->axiosHome
![[Pasted image 20220909201154.png]]
service-->modules-->jHome
![[Pasted image 20220909201042.png]]
2homeSearch. vue
![[Pasted image 20220909201431.png]]
![[Pasted image 20220909201250.png]]

#### 2.1.7.1 检查数据是否获取成功
1. console. log (hotSuggest) ![[Pasted image 20220909202715.png]]
2. vue 插件
![[Pasted image 20220909202814.png]]
#### 2.1.7.2 如果有的数据拿不到
1. ?.
![[Pasted image 20220910162912.png]]
2. v-if
![[Pasted image 20220910163541.png]]

### 2.1.8 滚动页面加载
1. window 窗口滚动
view-->home.vue
![[Pasted image 20220912124020.png]]
hooks-->useScroll
```js
import { throttle } from 'underscore'
import { onMounted,onUnmounted,ref } from 'vue'
//throttle 节流  debounce 防抖

export default function useScroll() {
  const isReachBottom = ref(false)

  const clientHeight = ref(0)
  const scrollTop = ref(0)
  const scrollHeight = ref(0)

  const scrollListenerHandler = throttle(() => {
    clientHeight.value = document.documentElement.clientHeight
    scrollTop.value = document.documentElement.scrollTop
    scrollHeight.value = document.documentElement.scrollHeight

    console.log(isReachBottom.value, clientHeight.value, scrollTop.value, scrollHeight.value )

    if (clientHeight.value + scrollTop.value >= scrollHeight.value) {
      console.log("bottom")
      isReachBottom.value = true
    }
  },100)
onMounted(() => {
  window.addEventListener("scroll",scrollListenerHandler)
})
onUnmounted(() => {
  window.addEventListener("scroll",scrollListenerHandler)
})

  return {isReachBottom,clientHeight,scrollTop,scrollHeight}
}
```

2. 元素滚动

### 2.1.9 watch 和 computed
- 监听并执行代码操作用 watch
- 定义一个依赖另一个响应式数据的响应式数据用 computed

### 2.1.10 日期数据共享
utils-->dayjs.js
![[Pasted image 20220912131849.png]]
将日期放在 store 状态管理里面
store-->module-->mianStore
![[Pasted image 20220912131746.png]]
使用
components-->topFix.vue
```js
<template>
  <div class="profile">
    <h3>profile</h3>
    <div>{{startDateStr}}</div>
    <div>{{endDateStr}}</div>
    <div>{{countDay}}</div>
  </div>
</template>

<script setup>
import useMainStore from '@/stores/modules/mainStore';
import { getDay, getDiffDays } from '@/utils/dayjs'
import { storeToRefs } from 'pinia';
import { computed } from '@vue/reactivity';

const mainStore = useMainStore()
const { startDate, endDate } = storeToRefs(mainStore)
const startDateStr = computed(() =>
  getDay(startDate.value)
)
const endDateStr = computed(() =>
  getDay(endDate.value)
)
const countDay = computed(() =>
  getDiffDays(startDate.value,endDate.value)
)

</script>

<style lang="less"  scoped>

</style>
```

### 2.1.11 loading
App. vue
```js
<template>
  <div class="App">
      <loading></loading>
  </div>
</template>

<script setup>
import loading from './components/loading.vue'
</script>

<style lang="less"  scoped>
  
</style>
```

components-->loading
![[Pasted image 20220912153650.png]]
service-->request-->j
![[Pasted image 20220912154820.png]]

### 2.1.12   [[03_组件间通讯]]
如果子组件只有一个根元素, 那么在父组件绑定的 class/click 等会默认加在根元素上; 如果子组件有多个元素则需要指明加在那个跟元素是哪个$atrr


## 2.2 难点 
### 2.2.1 展示数据在不同的tab
![[Pasted image 20220908003523.png]]
3searchCity.vue
![[Pasted image 20220909112620.png]]
setup
![[Pasted image 20220909113105.png]]
4searchCityGroup.vue
![[Pasted image 20220909112941.png]]
![[Pasted image 20220909113036.png]]

### 2.2.2 动态索引 
不展示没有的索引), 并添加#索引 (list. unshift ("#")
4searchCityGroup.vue
![[Pasted image 20220909115138.png]]

![[Pasted image 20220909115155.png]]
### 2.2.3 监听城市点击后跳转
4searchCityGroup.vue
![[Pasted image 20220909115630.png]]
axiosCity. js
![[Pasted image 20220909120759.png]]

数据衔接 (显示点击的城市)
hom-search. vue
![[Pasted image 20220909121238.png]]
![[Pasted image 20220909121252.png]]





----

# 3 问题:

## 3.1 请求数据拿到空数组怎么办 
- [ ]  Q:
![[Pasted image 20220909234401.png]]

- [ ]  A:



## 3.2 服务器返回很多数据 #面试题
当服务器返回很多数据时 (如: 几十万条数据), 前端的处理办法
1. 多线程
2. 虚拟列表
需要注意的是, 返回数据过多容易造成卡顿, 最好是由服务器先将数据处理好之后再传给前端

服务器处理好后的大量数据展示方法
 分页
 传参数形式
 1. page
 2. size (每次请求数据的个数)/ offsset (迁移量, 从取过的数据后面开始取)
![[Pasted image 20220910002115.png]]


## 3.3 能否三端都较好适应

 