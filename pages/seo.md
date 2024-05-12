## 使用 SSR

项目中使用 `Next.js` 这种 SSR 框架进行实现。通过前后端不分离的方式，服务端将 `HTML` 拼接完返回到前端，方便谷歌爬虫进行索引生成。
比如 ShipFast 的网站中，可以从 `Doc` 资源直接获取到数据，而不是通过 JS 在前端计算生成的。

![](/2.png)

如果是前后端分离的话，这些实时数据应该是获取不到的，是通过 JS 发起请求动态设置而成的，这一内容爬虫获取不到也无法生成索引

## Sitemap

学习 ahrefs 的官方教程，快速扫盲了一下 SEO 这一块的知识。其中有提到帮助谷歌更好地收录自己站点的方法有设置 Sitemap
![](/3.png)

尝试了一下，发现 SoraWebUI 中确实设置了 sitemap 和 robots.txt ～

![](/8.png)

## 参考资料

- [ahrefs 的 SEO 基础教程](https://ahrefs.com/seo)
- [从 SSR 到 SEO](https://juejin.cn/post/7095049421158612999)
