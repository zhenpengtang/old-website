---
layout: page
title: Raspberry Pi 变身移动路由器
---

想diy一个移动路由器，有shadowsocks功能的于是就做出来了

# RaspberryPi 变身移动路由器

材料：

* Huawei e180 3g modem
* RaspberryPi B+
* 无线网卡
* Debian

软件安装
<pre><code>
sudo apt-get update
sudo apt-get install wvdial supervisor hostapd dnsmasq openvpn
</code></pre>



<pre><code>
$cat forward.sh
#!/bin/bash
iptables -t nat -A POSTROUTING -o ppp0 -j MASQUERADE
echo 1 > /proc/sys/net/ipv4/ip_forward
</code></pre>

<pre><code>
$cat /etc/hostapd/hostapd.conf
interface=wlan0
driver=nl80211
ssid=RaspWiFi_T0
hw_mode=g
channel=11
wpa=2
wpa_passphrase=totolovelink
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP CCMP
wpa_ptk_rekey=600
macaddr_acl=0
</code></pre>


<pre><code>
在dnsmasq.conf最后面加入
interface=wlan0
dhcp-range=192.168.200.100,192.168.200.200,255.255.255.0,12h
</code></pre>


<pre><code>
加入到/etc/default/hostapd
DAEMON_CONF="/etc/hostapd/hostapd.conf"
</code></pre>


<pre><code>
加入到/etc/network/interface
auto wlan0
iface wlan0 inet static
address 192.168.200.1
netmask 255.255.255.0
</code></pre>

<pre><code>
在/etc/supersior/supervisord.conf最后加入
[program:wvdial]
command=wvdial
autostart=false
[program:wvdial-daemon]
command=/home/pi/wvdial-daemon.sh
autostart=true
autorestart=true
[program:forward]
command=/home/pi/forward.sh
autostart=true
</code></pre>


<pre><code>
$ cat wvdial-daemon.sh
#!/bin/bash
HOST=www.baidu.com
COUNT=30

mainapp(){
precent=`ping -s 1 -c 1 -W 1 $HOST`
if [ $? = 2 ];then
supervisorctl start wvdial
sleep 10
time=`uptime |awk '{print $1}'`
echo $time,"Start wvdial success"
fi
}

while true
do
mainapp
done</code></pre>

<pre><code>
</code></pre>

<pre><code>
</code></pre>

<pre><code>
</code></pre>
