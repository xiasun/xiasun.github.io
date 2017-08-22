---
title: ShadowSocks Client Installation and Proxy Configuration on Ubuntu 16.04
date: 2016-09-21 10:45:50
tags: Network;
---
I recently switched to ShadowSocks (Client) from different kinds of VPN clients, those VPNs never last long and often have unstable connection.

Using ShadowSocks on Windows is pretty easy, we just have to run a GUI and do some server configuration on it, the client would automatically start system proxy. However, let ShadowSocks works properly on Ubuntu do require some works. This post assumes no prior environment installed & configured except Ubuntu itself (ShadowSocks server access is required, you could buy one or set up one yourself).

## Step 1: Install ShadowSocks through PIP
ShadowSocks installed from apt-get is of low version and cannot support many password method, I recommend a installation using PIP.
Install PIP:
```bash
sudo apt-get install python-pip
```
Install ShadowSocks through PIP
```bash
pip install shadowsocks
```

---

## Step 2: ShadowSocks clients configuration
After installed ShadowSocks we have to set server IP, password and many arguments for a proper connection, you may configure it using Terminal commands, but I recommend creating a configuration file.
Create a ShadowSocks configuration file (json) and put it somewhere you like with content below
```bash
{
"server": "for.example.xyz",
"server_port": 10644,
"local_port": 1080,
"password": "123456",
"timeout": 600,
"method": "rc4-md5"
}
```
Now you can start your ShadowSocks client through command below
```bash
sslocal -c path/to/your/configuration/file/created/above start
```

---

## Step 3.1: Firefox proxy configuration
ShadowSocks follows socks5 proxy, so we cannot directly access http pages. Firefox is the default browser of ubuntu, so we first have to configure proxy on it.
<img src="2016/09/21/ubuntu-ss-notes/firefox-proxy-configure.jpg" width="75%" height="75%" alt="Firefox proxy configuration" title="Firefox proxy configuration">
Go to "Preference->Advanced->Network->Connection->Setting", select "Manual proxy configuration" and enter ShadowSocks default socks host 127.0.0.1 with port 1080, don't forget to select the "SOCKS v5" checkbox.

---

## Step 3.2: Chrome proxy configuration
After configure proper proxy on Firefox, you may want to use Chrome now. First download and install Chrome from Firefox (you may use apt-get but for these commonly-used and well-developed software I prefer to download from browser directly). Then we need a proxy management plugin, I recommend Switch Omega. However, install Chrome plugin requires connection to google which is not easy somewhere, so we first use Terminal command below to configure chrome proxy to conncect Google.
```bash
google-chrome --proxy-server=socks5://127.0.0.1:1080
```
Now chrome is started with proxy above. Now search for Switch Omega in Google Chrome App Center and install it. After install Switch Omega on Chrome, configure our socks5 proxy in it like below.
{% asset_img chrome-proxy-configure.jpg Chrome proxy configuration %}
Now next time you could start Chrome freely and use proxy to connect google.

---
## Reference
I learned skills above from this two post, list here for you to reference:

[Ubuntu14.04使用Shadowsocks及转换HTTP代理 – 蔓草札记](http://xuhehuan.com/2119.html)
[Linux Ubuntu桌面系统下使用shadowsocks 安装chrome](http://www.8dlive.com/post/168.html)
