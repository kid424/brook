# 例子

下面列举一些常用场景命令的例子, 注意自己替换示例中的 IP，端口，密码，域名，证书路径等参数

## 运行 brook server

```
brook server --listen :9999 --password hello
```

然后

-   server: `1.2.3.4:9999`
-   password: `hello`

或 获取 brook link

```
brook link --server 1.2.3.4:9999 --password hello --name 'my brook server'
```

或 获取 brook link 让 udp 走 tcp `--udpovertcp`

```
brook link --server 1.2.3.4:9999 --password hello --udpovertcp --name 'my brook server'
```

## 运行 brook wsserver

```
brook wsserver --listen :9999 --password hello
```

然后

-   server: `ws://1.2.3.4:9999`
-   password: `hello`

或 获取 brook link

```
brook link --server ws://1.2.3.4:9999 --password hello --name 'my brook wsserver'
```

或 获取 brook link 指定个域名, 甚至不是你自己的域名也可以

```
brook link --server ws://hello.com:9999 --password hello --address 1.2.3.4:9999 --name 'my brook wsserver'
```

## 运行 brook wssserver: 自动签发信任证书

> 注意：确保你的域名已成功解析到你服务器的 IP, 自动签发证书需要额外监听 80 端口

```
brook wssserver --domainaddress domain.com:443 --password hello
```

然后

-   server: `wss://domain.com:443`
-   password: `hello`

或 获取 brook link

```
brook link --server wss://domain.com:443 --password hello --name 'my brook wssserver'
```

## 运行 brook wssserver 使用已有的信任机构签发的证书

> 注意：确保你的域名已成功解析到你服务器的 IP

```
brook wssserver --domainaddress domain.com:443 --password hello --cert /root/cert.pem --certkey /root/certkey.pem
```

然后

-   server: `wss://domain.com:443`
-   password: `hello`

或 获取 brook link

```
brook link --server wss://domain.com:443 --password hello --name 'my brook wssserver'
```

## 运行 brook wssserver 自己签发非信任证书, 甚至不是你自己的域名也可以

安装 [mad](https://github.com/txthinking/mad)

```
nami install mad
```

使用 mad 生成根证书

```
mad ca --ca /root/ca.pem --key /root/cakey.pem
```

使用 mad 由根证书派发 domain.com 证书

```
mad cert --ca /root/ca.pem --ca_key /root/cakey.pem --cert /root/cert.pem --key /root/certkey.pem --domain domain.com
```

运行 brook

```
brook wssserver --domainaddress domain.com:443 --password hello --cert /root/cert.pem --certkey /root/certkey.pem
```

获取 brook link 使用 `--insecure`

```
brook link --server wss://domain.com:443 --password hello --name 'my brook wssserver' --address 1.2.3.4:443 --insecure
```

或 获取 brook link 使用 `--ca`

```
brook link --server wss://domain.com:443 --password hello --name 'my brook wssserver' --address 1.2.3.4:443 --ca /root/ca.pem
```

## withoutBrookProtocol

性能更好，但数据不使用 Brook 协议进行强加密。所以请使用证书加密，并且不建议--withoutBrookProtocol 和--insecure 一起使用

## withoutBrookProtocol 自动签发信任证书

> 注意：确保你的域名已成功解析到你服务器的 IP, 自动签发证书需要额外监听 80 端口

```
brook wssserver --domainaddress domain.com:443 --password hello --withoutBrookProtocol
```

获取 brook link

```
brook link --server wss://domain.com:443 --password hello --withoutBrookProtocol
```

## withoutBrookProtocol 使用已有的信任机构签发的证书

> 注意：确保你的域名已成功解析到你服务器的 IP

```
brook wssserver --domainaddress domain.com:443 --password hello --cert /root/cert.pem --certkey /root/certkey.pem --withoutBrookProtocol
```

获取 brook link

```
brook link --server wss://domain.com:443 --password hello --name 'my brook wssserver' --withoutBrookProtocol
```

## withoutBrookProtocol 自己签发非信任证书, 甚至不是你自己的域名也可以

安装 [mad](https://github.com/txthinking/mad)

```
nami install mad
```

使用 mad 生成根证书

```
mad ca --ca /root/ca.pem --key /root/cakey.pem
```

使用 mad 由根证书派发 domain.com 证书

```
mad cert --ca /root/ca.pem --ca_key /root/cakey.pem --cert /root/cert.pem --key /root/certkey.pem --domain domain.com
```

运行 brook wssserver

```
brook wssserver --domainaddress domain.com:443 --password hello --cert /root/cert.pem --certkey /root/certkey.pem --withoutBrookProtocol
```

获取 brook link

```
brook link --server wss://domain.com:443 --password hello --withoutBrookProtocol --address 1.2.3.4:443 --ca /root/ca.pem
```

## 运行 brook socks5, 一个独立的标准 socks5 server

```
brook socks5 --listen :1080 --socks5ServerIP 1.2.3.4
```

然后

-   server: `1.2.3.4:1080`

或 获取 brook link

```
brook link --server socks5://1.2.3.4:1080
```

## 运行 brook socks5, 一个独立的标准 socks5 server, 指定用户名和密码

```
brook socks5 --listen :1080 --socks5ServerIP 1.2.3.4 --username hello --password world
```

然后

-   server: `1.2.3.4:1080`
-   username: `hello`
-   password: `world`

或 获取 brook link

```
brook link --server socks5://1.2.3.4:1080 --username hello --password world
```

## brook relayoverbrook 中继任何 TCP 和 UDP server, 让其走 brook 协议. 它与 brook server wsserver wssserver 一起工作

```
brook relayoverbrook ... --from 127.0.0.1:5353 --to 8.8.8.8:53
```

## brook dnsserveroverbrook 用来创建一个加密 DNS Server, TCP and UDP, 它与 brook server wsserver wssserver 一起工作

```
brook dnsserveroverbrook ... --listen 127.0.0.1:53
```

## Brook OpenWRT 路由器，完美支持 IPv4/IPv6/TCP/UDP，Native IPv6

https://www.txthinking.com/talks/articles/brook-openwrt.article

## 使用 Brook 把 macOS 变成网关

https://www.txthinking.com/talks/articles/brook-macos-gateway.article

## 使用 Brook 把 Windows 变成网关

https://www.txthinking.com/talks/articles/brook-windows-gateway.article

## 使用 Brook 把 Linux 变成网关

https://www.txthinking.com/talks/articles/brook-linux-gateway.article

## brook relay 可以中继任何 TCP 和 UDP server, 这是一个独立的功能, 它不依赖 brook server wsserver wssserver

```
brook relay --from :9999 --to 1.2.3.4:9999
```

## brook socks5tohttp 将 socks5 proxy 转换为 http proxy

```
brook socks5tohttp --socks5 127.0.0.1:1080 --listen 127.0.0.1:8010
```

## brook pac 创建一个 pac server

```
brook pac --listen 127.0.0.1:8080 --proxy 'SOCKS5 127.0.0.1:1080; SOCKS 127.0.0.1:1080; DIRECT' --bypassDomainList ...
```

## brook pac 创建一个 pac 文件

```
brook pac --file proxy.pac --proxy 'SOCKS5 127.0.0.1:1080; SOCKS 127.0.0.1:1080; DIRECT' --bypassDomainList ...
```

## 例子不胜枚举，更多功能建议挨个看 CLI 文档的命令和参数吧，还有博客，YouTube 等...
