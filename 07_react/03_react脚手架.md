# 脚手架 scaffold
## 安装
npm i create-react-app -g

创建项目
create-react-app 项目名

注意: 项目名不能包含大写字母, 且不能为中文

## 目录结构
![[Pasted image 20221011223235.png]]

PWA
https://developer.mozilla.org/zh-CN/docs/Web/Progressive_web_apps
PWA 全称 Progressive Web App，即渐进式 WEB 应用；

- 可以将 web 内容添加至手机的主屏幕 (App manifast)
- 离线缓存功能 (service worker)
- 消息推送

## react 脚手架中的 webpack
调出 webpack 中的配置文件
eject-->弹出
npm run eject (不推荐)
craco (create-react-app config ) 是更好的配置方法

![[Pasted image 20221011224549.png]]