# 项目背景

Sorawebui 是通过集成 OpenAI 的 Sora 模型，本项目为用户提供了一个直观且高效的在线平台，让他们能够轻松地将文本转化为生动的视频内容。

- 支持国际化多语言功能
- 集成 Sora 模型，在线生成视频
  ![](/10.png)

# 为什么使用 Next.js

> Next.js 是一个基于 React 的服务端渲染框架。

- 服务端渲染 (SSR) 和预渲染 (SSG)：有利于更好的 SEO 和提高页面加载速度
- 加载速度快：支持预渲染和 SSR，减少了客户端加载的时间。
- 热更新：支持 HMR 热更新，能够在开发程序修改代码的同时，立即看到效果变化，无需刷新页面。
- 部署简单：可以借助 Vercel、Netlify 等平台将应用程序快速部署到云端，或者将其部署到自己的服务器上。
- 生态成熟：拥有庞大的社区和丰富的插件，扩展和工具支持。
  Next.js 还有许多优点和便利之处，简而言之，它能使 React 应用开发更加简单和快速。

# 项目目录结构

每个文件夹表示一个路由，映射到一个 URL
![](/11.png)

# 路由

Next 中的每一个文件夹都代表着一个路由
![](/12.png)

- 动态路由：可以通过方括号来创建动态路由区段，例如在项目中为了实现多语言的功能，一级路由中使用[locale]进行动态段的声明。
- 重定向：能够使用户重定向到另一个 URL 中，在项目中根页面中使用了重定向方法

```jsx
import { redirect } from 'next/navigation'

// This page only renders when the app is built statically (output: 'export')

export default function RootPage() {
  redirect('/en')
}
```

# 数据获取

在本项目中，使用了 fetch 和路由处理程序 来进行数据获取。

### 路由处理程序

在 Next 中，允许使用 Web 请求或者调用 Api 给定路由创建自定义处理程序，它的路由等同于它在文件中的路径。
简单来说就是，我们可以使用 Next 来创建一个前后端一体化的全栈项目。
在项目中，使用路由处理来对视频生成进行了处理，调取外部 Sora 模型提供的接口。

![](/13.png) >对三方接口进行封装，能够保证关键数据的隐私性与安全性。后期也能够更好地对接口进行集中的加工处理。

### fetch 方法

在 Next 中，扩展了本机的 fetch API ，它能够在渲染组件树时，自动记住获取请求。

## 优化

### Images

在 Next 中，可以使用 Image 组件替代原生的<img>标签，它扩展了原生功能，具有图像自动优化的效果。
优点：

- 大小优化：可以根据不同终端尺寸，匹配提供正确大小的图像
- 视觉稳定
- 更快的页面加载
  使用组件 Image 组件时，只需提前导入该组件，其内置属性与原生标签类似。

```
import Image from "next/image";

<Image

className="h-10"

src="/appicon.svg"

width={32}

height={32}

alt="Sorawebui.com"

/>
```

### Link

\<Link> 是一个 React 组件，扩展了\<a> 的功能。

#### \<Link>与\<a>的不同？

\<Link> 的原理其实最终还是创建\<a>，只不过创建时它还同时监听了点击事件。
点击事件做了两件事情：

- 如果监听事件有绑定函数，则执行该函数
- 接下来，会判断是否阻止\<a>的默认跳转，阻止的话。根据 replace 的 props 值决定执行 history.push 还是执行 history.replace。