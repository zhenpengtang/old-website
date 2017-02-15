---
layout: post
title: web上显示你的android手机上的短信
---
## 效果图

 `![](my_pics/2017_02_15_14.40.10_Ink_LI.jpg)`

## 材料：
* Anroid手机一部带SIM卡能上网
* iPhone手机一部能上网
* 公网能连接的address & port

## 功能：
* 可以在iPhone上查看你的Android的短信

## 免费测试
1. 发送一条有test字符的短信到17620388002
2. 然后打开[测试页](http://103.253.25.63:7777/showyoursms)

## 前言
我有一个移动号要收短信，联通号用来上网。带两个手机好麻烦。
那我就带iphone加联通号上网。又要查看移动的短信。
用过好多方法tasker+ pushbullet 有时候会断线收不到。
tasker+直接短信转发，成本高。tasker+http+twilio,多了个twilio也麻烦，
后来就直接做http post上服务器，看的时候get 一下 。
用的tornado +bootstrap简单一点，css不会啊，好丑啊。将就用一下吧。
有朋友能帮我弄好看，请联系，有不会的，我也会耐心教的。

## 实现功能
android手机收到短信先POST到服务器，再从pushbullet发送到iphone

## 免费测试
上我的网站看短信。我的短信经过过滤。可能发短信到我的手机号测试
只须要发一条有test的短信你就可以在网页上看到的，没有免费短信慎发
 
### 用法：发送一条有test字符的短信到17620388002

### 然后打开[测试页](http://103.253.25.63:7777/showyoursms)




## 服务器端

SMSInbox

```
git clone http://zhenpengtang.github.com/SMSInbox
```

#### 注意建议局域网测试先

```bash
$cd SMSInbox
$python app
```

#### 打开连接[测试页](http://linux_ip_address:8888/showyoursms)有显示代表成功了

## 客户端Android
下载叫tasker的神器，安装好运行

以下是步骤:

+号>事件>电话>收到短信>任意改短信，按返回>新建任务>输入任务名>+号>网络>HTTP POST

* 服务器:端口 
> linux_ip_address:8888

* 路径: 
>test

* 数据:
> post_token=xxxanother_md5sumxxx
> number=xxxxx
> text=xxxxxx
> datetime=xxxxx


最后按下面左边的三角号,发射
打开link看看http://linux_ip_address:8888/test?get_token=xxxmd5sumxxx


