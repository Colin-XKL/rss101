
## 0x02 获取 Feed 文章全文

部分 RSS 源并不会在 xml 文件内提供文章全文，说白了是想让你点进他们的网站去浏览，这样网页上的广告才有可能被你点击。解决的方案有很多，方便起见我使用了 TTRSS 的插件 Readability 和 Mercury。两者都不能完美适配所有站点，同时启用这两者以实现互补。

## 0x03 无障碍阅读繁体中文 Feed

发现了几个质量不错的繁体中文信息源，主要是台湾的站点，如泛科学。由于文字和部分两岸文化差异，直接阅读繁体中文的文章有些困难。我的解决方案是使用 OpenCC 简繁转换服务，它能够对可映射的简繁汉字以及同一事物的两岸不同的表述进行翻译，输出的简体中文版文章基本可以无障碍阅读。Awesome-TTRSS 内有集成相应的插件和服务程序。

不过原作者是使用 node.js 编写的服务端，翻译数据库得不到及时更新，如翻译后还是写的是`义大利`而不是`意大利`。而且 docker image 体积 100+M，内存占用也较大。我在考虑用 Go 语言重写 OpenCC 的服务端并兼容 TTRSS 的 OpenCC 插件。

https://github.com/Colin-XKL/opencc-api-go

## 订阅海外RSS 源
由于众所周知的原因，我国的互联网是不「互联」的。rsshub.app 部署在国外，现已基本无法直接访问。国内服务器上自建的 RSSHub 订阅如 Facebook 等国外站点更是不可行。为此我使用了 Clash 代理，并添加了一些公开的机场订阅，虽然速度和稳定性不是很高，但对于 RSS 这种需求还是绰绰有余的。又完善了一些爬墙的规则，比如对 google、facebook，rsshub.app 走代理，内网地址和 CN 的 IP 直连，反爬严格的网站完全走随机节点。一番操作下来，基本可以实现全球 RSS 订阅自由了 