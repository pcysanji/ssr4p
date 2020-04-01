# ssr4p
ShadowsocksR 的用户自定义规则 user.rule

感谢ACL4SSR的规则，此版本是自己使用中补充的一些规则 BY 静海流沙

## 适用客户端
适用于SSR C#客户端，如以下版本

- [Anankke/shadowsocksr-csharp](https://github.com/shadowsocksrr/shadowsocksr-csharp/releases)

- [ssr 4.9.2 tlanyan修复版](https://tlanyan.me/shadowsockr-shadowsocksr-shadowsocksrr-clients/)

- [HMBSbige/ShadowsocksR-Windows](https://github.com/HMBSbige/ShadowsocksR-Windows/)

- [SSRR-Windows](https://github.com/Anankke/SSRR-Windows)

> By ACL4SSR - 
> 屏蔽常用网站、视频、手机rom广告&运营商劫持广告&数据跟踪&开屏广告
>
> 参照lhie1大神的surge规则改编，致谢!! https://github.com/lhie1/Surge
>
> 参照scomper大神的surge规则改编，致谢!! https://gist.github.com/scomper/915b04a974f9e11952babfd0bbb241a8/revisions

## 使用说明
1. 放在ShadowsocksR 软件根目录
2. 系统代理使用全局，规则设置>代理规则，使用用户自定义。
3. 如果非要使用 PAC，建议更新 pac 规则为绕过局域网和IP。这样相当于在 PAC 黑名单的基础上加了一个用户规则白名单。

## 原理说明
shadowsocksR 一般通过 PAC.txt 分流代理，用户在 user-rule.txt 添加自己的 PAC 规则。后来添加了代理规则模式，可选择用户自定义，则自动调用 user.rule 进行分流。

- 在**全局模式**下，代理规则选择用户自定义，网络流量通过 shadowsocksR，shadowsocksR 通过  user.rule 判断哪些需要走代理，哪些需要直连，哪些需要拒绝连接，哪些需要本地代理。

- 在**PAC模式**下，代理规则选择用户自定义，网络流量先通过 PAC 判断哪些流量可以流向 shadowsocksR，shadowsocksR 通过  user.rule 判断哪些需要走代理，哪些需要直连，哪些需要拒绝连接，哪些需要本地代理。

我个人认为 user.rule 的语法更为简单和灵活，所以逐渐采用此分流方式。

### 规则匹配结果类型
user.rule 提供规则四种匹配结果类型 ：**remoteproxy、localproxy、direct、reject**

- remoteproxy：经过SSR服务器连接（走代理）
- localproxy：经过本地代理连接，或没有配置本地代理时使用直连连接（本地代理指的是：选项设置 - 二级(前置)代理）
- direct：直接连接（直连，不走代理）
- reject：拒绝连接（可用于屏蔽广告，当然前提是用系统代理规则：全局模式，否则只有进入SSR客户端的广告才会被过滤）

### 基本规则
规则文件内，除了空行和注释，其它的每行都是一条规则，规则之间有**先后次序**之分。若出现相同的规则，那么后一条规则可覆盖前一条规则。

规则分两类：

- 域名规则
- IP段规则


### 写法实例
.google.com remoteproxy # .google.com 后缀的所有网址都走代理

59.24.3.174 59.24.3.225 remoteproxy # 59.24.3.174 到 59.24.3.225的IP段都走代理


官方教程：https://github.com/shadowsocksrr/shadowsocks-rss/wiki/C%23-Proxy-Rule


## 下载地址
https://raw.githubusercontent.com/pcysanji/ssr4p/master/user.rule
