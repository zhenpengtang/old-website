---
layout: post
title: Web上显示你的android手机上的短信
---

### On your linux

SMSInbox
```
git clone http://zhenpengtang.github.com/SMSInbox
```

#### 注意
* 建议局域网测试先


```bash
$cd SMSInbox
$python app
```

打开连接

http://linux_ip_address:8888/showyoursms

http://linux_ip_address:8888/test?get_token=xxxmd5sumxxx


有显示代表成功了


下一步
### On android phone

下载叫tasker的神器，安装好运行

以下是步骤:

+号>事件>电话>收到短信>任意改短信，按返回>新建任务>输入任务名>+号>网络>HTTP POST>
* 服务器:端口 `linux_ip_address:8888`
* 路径: `test`
* 数据:
```
post_token=xxxanother_md5sumxxx
number=xxxxx
text=xxxxxx
datetime=xxxxx
```

最后按下面左边的三角号,发射

打开link看看

http://linux_ip_address:8888/test?get_token=xxxmd5sumxxx
