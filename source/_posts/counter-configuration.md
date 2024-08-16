---
title: hexo+fluid+leancloud添加访问量显示（图文）
date: 2024-08-15 23:24:56
index_img: https://mediacdn.uuu.me.uk/imgs/2024-8-15/img254-index.jpg
banner_img: https://mediacdn.uuu.me.uk/imgs/2024-8-15/img254.webp
tags:
---
最近心血来潮，给博客加了个访问量显示，在这里记录下过程。
## 配置Leancloud
注册账号我就不讲了，很简单，几分钟可以搞定。
### 创建应用
点击账户主页上的“创建应用”。
![创建应用](https://mediacdn.uuu.me.uk/imgs/2024-8-15/1.png "创建应用")
随便填写一个应用名称，计价方案选择开发版，描述可加可不加，最后，点击”创建“。
![配置应用](https://mediacdn.uuu.me.uk/imgs/2024-8-15/2.png "配置应用")
应用创建完成后，点击”设置“---->"安全中心"---->在“Web安全域名”下添加你的博客地址，避免请求被拒绝。
![添加白名单](https://mediacdn.uuu.me.uk/imgs/2024-8-15/3.png "添加白名单")
点击“应用凭证”，复制appid和appkey（后面要用到）
![复制凭证](https://mediacdn.uuu.me.uk/imgs/2024-8-15/7.png "复制凭证")
### 绑定自定义域名
原因请看[这里](https://github.com/orgs/walinejs/discussions/1203)。
点击“域名绑定”--->“绑定新域名”。
![绑定域名](https://mediacdn.uuu.me.uk/imgs/2024-8-15/4.png "绑定域名")
在弹出的窗口中，输入你想绑定的域名，然后点击绑定按钮。
![输入域名](https://mediacdn.uuu.me.uk/imgs/2024-8-15/5.png "输入域名")
完成后，请复制CNAME解析配置，到DNS提供商配置对应的CNAME记录。
![配置域名](https://mediacdn.uuu.me.uk/imgs/2024-8-15/6.png "配置域名")
## 配置主题
在博客的主题配置文件中，找到`web_analytics`，修改`enable`、`app_id`和`app_key`：
```yaml
web_analytics:
  enable: false # 改为true
  baidu:
  google:
  tencent:
    sid:
    cid:
  woyaola:
  cnzz:
  leancloud:
    app_id: # 填appid
    app_key: # 填appkey
    server_url:  # 填刚才绑定的域名 https://example.example.com
```
再找到`footer`，修改`enable`和`source`：
```yaml
footer:
  statistics:
    enable: true # 改为true
    source: "leancloud"  # 改为leancloud
    # 如果没有pv_format和uv_format，请手动添加
    pv_format: "总访问量 {} 次"  # 这里{}代表访问量，下面{}代表访客数
    uv_format: "总访客数 {} 人"
```
## 大功告成
在博客目录运行以下命令，重新部署博客：
```
hexo g
hexo d
```
Enjoy it!(๑•̀ㅂ•́)و✧
![效果图](https://mediacdn.uuu.me.uk/imgs/2024-8-15/8.png "效果图")
