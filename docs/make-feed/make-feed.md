
繁茂如 RSSHub 也不能保证拥有所有站点的 RSS 源。对于自制源，网上的方案大多数为使用 Feed43 和 Feedburner，但是人家是商业服务，虽然使用确实方便，但说到底还是为了商业。白嫖用户限制多不说，天知道哪天会有 break change 或者直接被墙或者跑路。最稳妥的做法还是自建。

手写爬虫程序简单灵活，不过后期维护难度较高而且难以复用。对于我想要订阅而有没有现成的源的网站，我的解决方案主要是两个：

### 1. 为 RSSHub 编写目标站点的规则，并 Pull Request 申请合并

RSSHub 除了提供众多现成的各类站点的 RSS 规则之外，也提供了快速构建一个站点的 RSS 源的常用工具类和模板。需要对 JavaScript 和爬虫技术有一定了解。很荣幸能提交了几个 pr 并且已经合并进了主分支，如 [知乎的用户文章列表](https://docs.rsshub.app/social-media.html#zhi-hu-yong-hu-wen-zhang)。

### 2. 使用 Huginn 为目标站点自制源

[Huginn](https://github.com/huginn/huginn) 是一个强大的 [IFTTT](https://sspai.com/post/25270#!) 应用，用它来生成 RSS 源简直是大材小用（主要是他动辄 200M 的内存占用）。不过某些情况下我需要监视特定站点并在内容变化时得到通知，个人向为主，这类就不适合写 RSSHub 的规则。

使用门槛比 RSSHub 略低，可视化界面还是比较友好的，不过新手上手还是会有点困难，了解了 Huginn 的工作原理和基本的 Liquid 语法之后就手到擒来了。

### 3. 使用 feed43 和 rss-proxy 这类可视化工具自助生成 RSS 链接

手写解析规则还是太麻烦，很多网页结构很简单根本没必要单独花时间写一堆解析规则，而且有些时候只是想临时订阅一段时间或是订阅个很小的网站，不想大费周章，选择 feed43 这类工具不失为一个轻量又便捷的选择。不过[feed43](https://feed43.com/)对免费账户创建的 RSS 并不保证稳定，时常无法连接甚至直接失效。在 Github 上发现一个不错的替代品[rss-proxy](https://github.com/damoeb/rss-proxy/)，一个可视化的，快速自助生成站点 RSS 链接的工具。

![rss-proxy screenshot](https://cdn.jsdelivr.net/gh/damoeb/rss-proxy/docs/rssproxy-candidates.png)

填入目标网址就可以自动解析目标网页，程序会自动检测网页上的列表内容，可以自己选择要订阅哪个列表，然后就可以生成一个 RSS 链接。生成的 RSS 链接包括的信息有目标网址、要订阅的目标列表的节点信息和输出格式（RSS/ATOM）等，也就是说，rss-proxy 并不像 feed43 会把解析的规则存储在服务端，它是直接编码在 url 里面的！rss-proxy 开源支持自部署，不想用它提供的公用实例也可以自建，迁移零门槛。rss-proxy 也支持调用无头浏览器渲染异步获取数据的网页，可玩性很高。

->>>> [rss-proxy 公用实例](https://rssproxy-v1.migor.org/)，可以点击体验下，还是很方便的

使用了一段时间体验挺不错，有个小问题就是对 UTF-8 以外的编码不太友好。