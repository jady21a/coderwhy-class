# axios
axios 没有具体翻译, why 理解为:
axios: ajax i/o system. 
![[Pasted image 20220905223333.png]]
ajax 输入输出系统

vue create 创建的项目自带 axios, 不需要自己安装

功能: 
跨平台 (浏览器和 node 都可以用)
支持 promise api
拦截请求和拦截响应
转换请求和响应数据

## 网络请求测试接口网站
[httpbin.org](http://httpbin.org/)

## 请求方式
- axios (config)
- axios. request (config)
- axios. get (url [,config] )
- axios. post (url [, config] )
- axios. delete (url [, config] )
- axios. head (url [, config] )
- axios. put (url [, config] )
- axios. patch (url [, config] )
- axios. all  (有一个 reject 就 reject)

request+get
![[Pasted image 20220906004214.png]]
post
![[Pasted image 20220906004240.png]]
baseURL+axios. all
![[Pasted image 20220906004331.png]]

### config:
- url
- method: "get"/"post" (请求类型)
- baseURL:" http://www.vv.com/" (根路径)
- data : { key: 'aa'}  (request body)
- timeout: 1000 (超时设置)
- headers: {'x-Requested-With':'XMLHttpRequest'}}自定义的请求头
- param:{ id: 12 }, URL 查询对象 (如不同id)
- transformRequest:[function (data){}]请求前的数据处理
- transformResponse: [function (data){}]请求后的数据处理
- paramsSerializer: function (params){ } 查询对象序列化函数

## axios 创建多个实例
从 axios 模块中导入对象时, 使用的实例是默认的实例, 其配置也是固定的, 
要想自己更改配置信息, 就可以创建新实例来更改
![[Pasted image 20220906004138.png]]
## 拦截请求和拦截响应
interceptors. request 和 interceptors.response
![[Pasted image 20220906005318.png]]
#  封装自己的 axios (简洁版)
service. index
![[Pasted image 20220906010931.png]]
使用
04_jRequest
![[Pasted image 20220906011012.png]]
