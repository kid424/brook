# Getting Started

## Server

```
bash <(curl https://bash.ooo/nami.sh)
```

```
nami install brook
```

```
brook server -l :9999 -p hello
```

## GUI Client

| iOS | Android      | Mac    |Windows      |Linux        |OpenWrt      |
| --- | --- | --- | --- | --- | --- |
| [![](https://brook.app/images/appstore.png)](https://apps.apple.com/us/app/brook-network-tool/id1216002642) | [![](https://brook.app/images/android.png)](https://github.com/txthinking/brook/releases/latest/download/Brook.apk) | [![](https://brook.app/images/mac.png)](https://apps.apple.com/us/app/brook-network-tool/id1216002642) | [![Windows](https://brook.app/images/windows.png)](https://github.com/txthinking/brook/releases/latest/download/Brook.msix) | [![](https://brook.app/images/linux.png)](https://github.com/txthinking/brook/releases/latest/download/Brook.bin) | [![OpenWrt](https://brook.app/images/openwrt.png)](https://github.com/txthinking/brook/releases) |
| / | / | [App Mode](https://www.txthinking.com/talks/articles/macos-app-mode-en.article) | [How](https://www.txthinking.com/talks/articles/msix-brook-en.article) | [How](https://www.txthinking.com/talks/articles/linux-app-brook-en.article) | [How](https://www.txthinking.com/talks/articles/brook-openwrt-en.article) |
| / | / | [App 模式](https://www.txthinking.com/talks/articles/macos-app-mode.article) | [如何](https://www.txthinking.com/talks/articles/msix-brook.article) | [如何](https://www.txthinking.com/talks/articles/linux-app-brook.article) | [如何](https://www.txthinking.com/talks/articles/brook-openwrt.article) |

## CLI Client

```
brook client -s 1.2.3.4:9999 -p hello --socks5 127.0.0.1:1080
```
