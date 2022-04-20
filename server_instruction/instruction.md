# 个人搭建指南

**这篇文章写就于3年前，许多的技术已经发生了改变，因此请谨慎使用该教程**

## 服务器选择

一般来说，VPS 的虚拟化技术主流为 OpenVZ 与 KVM 架构，从各种资源以及 Shadowsocks 服务支持上，建议选择 KVM 架构的机器，以下所有的说明都是基于搬瓦工 KVM 建构的机器。

## 服务器系统

服务器建议安装带有BBR技术的Linux系统，TCP BBR 拥塞控制算法由 Google 开发，并提交到了 Linux 内核，从 4.9 开始，Linux 内核已经用上了该算法。根据以往的传统，Google 总是先在自家的生产环境上线运用后，才会将代码开源，此次也不例外。根据实地测试，在部署了最新版内核并开启了 TCP BBR 的机器上，网速甚至可以提升好几个数量级。

搬瓦工的机器可以在控制面板 ---> install new os ---> centos-7-x86_64-bbr，快速更换系统，注意备份服务器上的数据。

![](../image/newOS.png)

## Shadowsocks-libev

随着技术发展，Shadowsocks与墙之间的交锋也是一次比一次激烈，据传说，即使是Shadowsocks的256位加密，运营商可以做到解密，监视Shadowsocks使用者的上网流量，真实性未知，但小心点总不会错。

目前有4个衍生版本的Shadowsocks:

1. Shadowsocks-go: 二进制编译, 轻量, 快速
2. Shadowsocks-python: 无功无过，也是最原始的版本，近年来更新速度略慢
3. Shadowsocks-libev: 一直处于更新之中，最大的特点是支持obfs混淆
4. ShadowsocksR: 从作者到产品都极负争议性, obfs混淆模式开创者, 但是前一段时间SSR服务器普遍遭到GFW的封杀. 

现阶段为了能在安全与速度之间取得平衡，我个人更加推荐使用 Shadowsocks-libev + obfs混淆。

#### obfs 混淆

obfs 混淆最大的作用是对 Shadowsocks 流量进行伪装, 在不添加obfs的情况下, 运营商服务器通过的流量为未知的加密流量, 据说 GFW 已经有一定的包检测的能力, 仅仅加密流量具有一定的风险, 添加 obfs http 模式之后, 通过运营商的流量会被识别为设定好的网址的流量, 假设你设定的是 bing, 那么你的 Shadowsocks 流量会被判别为你当前正在访问 bing, 减少了被封杀的可能性，**tls模式安全性高于http模式**。

之前流量不是无限的时代, 因为只有运营商的 APP 可以无限使用流量, 比如什么天翼视讯, 利用 obfs 混淆, 可以将你的手机流量伪装为天翼视讯的流量, 从而达到无限使用使用流量, 这种操作太骚, 实测可以成功, 不过还是低调的好.

### Shadowsocks-libev 安装与配置

请注意，随着时间流逝，以下教程必然会过时，因此仅作为个人服务器搭建的参考。

安装图省心推荐秋水逸冰的[一键安装脚本](https://teddysun.com/357.html)

**请注意，秋水逸冰已经宣布放弃继续维护该脚本，因此该脚本可能随时会失效**

1. 使用 root 用户 SSH 登录

   ```shell
   wget --no-check-certificate -O shadowsocks-all.sh https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks-all.sh
   chmod +x shadowsocks-all.sh
   ./shadowsocks-all.sh 2>&1 | tee shadowsocks-all.log
   ```

2. 跟随提示选择相对应的模式即可

   1. 加密方式推荐 **chacha20-itef-poly1305**, 
   2. 端口可以尽量设置高一点,避免443, 1080等常用端口, 
   3. **安装 simple-obfs , 选择 http 模式**

   安装成功后会有如下提示:

   ```shell
   Congratulations, your_shadowsocks_version install completed!
   Your Server IP        :your_server_ip
   Your Server Port      :your_server_port
   Your Password         :your_password
   Your Encryption Method:your_encryption_method
   
   Your QR Code: (For Shadowsocks Windows, OSX, Android and iOS clients)
   ss://your_encryption_method:your_password@your_server_ip:your_server_port
   Your QR Code has been saved as a PNG file path:
    your_path.png
   
   Welcome to visit:https://teddysun.com/486.html
   Enjoy it!
   ```

   ![Snipaste_2018-09-12_09-12-18](../image/Snipaste_2018-09-12_09-12-18.png)

3. 卸载

   使用root用户登录

   ```shell
   ./shadowsocks-all.sh uninstall
   ```

4. 常用命令

   ```shell
   启动：/etc/init.d/shadowsocks-libev start
   停止：/etc/init.d/shadowsocks-libev stop
   重启：/etc/init.d/shadowsocks-libev restart
   查看状态：/etc/init.d/shadowsocks-libev status
   ```
   
5. 配置文件地址
   ```shell
   //etc/shadowsocks-libev/config.json
   ```
## Shadowsocks客户端

Shadowsocks 客户端已经全平台覆盖了, Github 上有专门的开源客户端项目.

### Windows

#### 下载地址

- [Win Shadowsocks客户端下载地址](https://github.com/shadowsocks/shadowsocks-windows/releases)
- [Shadowsocks obfs-local插件下载地址](https://github.com/shadowsocks/simple-obfs/releases)

#### 本地配置

服务器端已将安装了 obfs, 本地端直接下载obfs-local插件, 解压后**将插件 obfs-local 与Shdowsocks.exe 同一路径下**即可.

![](../image/Snipaste_2018-09-12_09-22-01.png)

obfs可以直接在Shadowsocks的服务器编辑页面修改参数

![](../image/Snipaste_2018-09-12_09-24-32.png)

插件选项为 **obfs=http;obfs-host=www.bing.com**, 实际上可以将 www.bing.com 更换为任意的一个网址, 只要不是被GFW封杀的就可以, 推荐像腾讯视频, 优酷, bing这种流量较大的网站, ~~如果填写是Google或者YouTube, 活着不好么......~~



### macOS

~~macOS上的Shadowsocks客户端目前似乎还是不支持obfs混淆.~~
2018/10/06更新
#### Shadowsocks-NG

GitHub上存在好几种Mac客户端，使用最广的是Shadowsocks-NG，目前的版本中已经支持obfs混淆，并且已经直接集成于客户端之中，无需额外下载，按照windows的设置填写参数即可。
![](../image/macOsNG.png)

- [Shadowsocks-NG 下载地址](https://github.com/shadowsocks/ShadowsocksX-NG/releases)

#### ClashX

最近出现了一个新的类Surge软件，ClashX，目前还在快速迭代期之中，兼容 Surge 的 config 文件，基本上对其稍作修改便可以导入 ClashX 中使用。可以去官方[ Telegram 群](t.me/clash_discuss)参与讨论

类Surge软件的核心都在于config文件，在Shadowsocks网络分流的基础上，对不同的流量产生不同的行为，可以实现指定网址代理，广告屏蔽等效果，自由度更高。

![](../image/clashX.png)

- [ClashX 下载地址](https://github.com/yichengchen/clashX/releases)

#### Surge

支持obfs混淆，在3.0版本中加入了全新的rule-set模式，config的管理从本地可以完全移至云端，不同的rule-set对应不同的应用规则，更容易管理，~~只可惜没钱截图😂~~

![](../image/Surge_Mac.png)

### iOS

iOS上推荐的客户端为 Shadowrocket 与 Surge, 首推  Shadowrocket, 因为便宜够用, 唯一遗憾的是国区下架了, 只能用非国区的 Apple ID 购买与下载, Surge3 目前可以在国区下载, 虽然 Surge 是配置文件类开创者, UI 更好看, 功能更强大,颇高的上手难度与 328 的价格会吓退不少人，但一句话，Surge 贵在稳定。

两款客户端均支持 obfs, Surge 2 与 Surge 3 均支持 tls  与 http 两种模式; shadowrocket 支持 http 与 tls 两种模式

2018年10月8日更新：Quantumult 最近热度也上来了，在小火箭与 Quantumult 任选其一既可。

#### Surge

Surge 在编辑服务器的 Advance 设置中可以配置混淆

![surge](../image/surge.png)

#### Shadowrocket

shadowrocket在服务器的编辑页面中即可设置混淆

![sr](../image/sr.png)

### Android

#### Shadowsocks

推荐在Google Play上下载Shadowsocks app, 同时下载obfs插件, 开发者均为 Max Lv. 

也可以前往 [Shadowsocks-Android](https://github.com/shadowsocks/shadowsocks-android/releases) 的 GitHub 仓库下载。

![](../image/ass.png)

#### Postern 

Postern 目前尚不支持混淆模式。
