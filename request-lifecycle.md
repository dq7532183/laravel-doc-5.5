# 请求生命周期

[TOC]

## #引言
在实际生活中使用工具时，如理解工具的原理，那么使用时也就会得心应手。 应用程序开发亦是如此。 如你理解了开发工具的结构和原理，开发时就会轻松加愉快。

本文档的目标就是让你对Laravel框架有个宏观的认识。 随着对框架越来越全面的认识，一切都不会再那么神秘， 同时我们在构建应用程序时也会越来越有信心。  切记，在不能马上理解那些全部的专业术语时，不要灰心。 试着先了解些基础功能，随着你对文档的探索逐步深入，你的知识也会随之增长。

## #生命周期概述

### 首要任务
Laravel应用程序的全部请求入口都是 *public/index.php* 文件。所有的请求应该被你的web服务器（Apache/Nginx）定位到该文件。*index.php* 文件不会包含大量的代码，而仅仅是加载框架其余部分的一个起始点。

*index.php* 文件会加载由Compser生成的自动加载，之后会从 *bootstrap/app.php* 中获取一个Laravel应用程序的实例。Laravel框架做的第一件事就是创建一个应用实例（也称作[服务容器](container)）。

### HTTP/Console内核
接下来，依据进入应用程序的请求类型不同，请求将会被发送到HTTP或Console内核。这两个内核提供的服务是请求流程处理的核心。现在，让我们把注意力放在HTTP内核上，HTTP内核由 *app/Http/Kernel.php* 定义。

HTTP内核继承自 *Illuinate\Foundation\Http\Kernel* 类, 该类定义了一个 *bootstrapers(启动项)* 数组, 会在请求处理前被执行。这些启动项包括配置错误处理器，配置日志，[探测应用程序环境]()，以及哪些需要在正式处理请求前执行的任务。

HTTP内核还定义了一些所有请求在被应用程序处理前执行的HTTP *中间件*。这些中间件用来处理 [Http Session]() 的读写，探测应用程序是否处于维护模式，[验证CSRF令牌]()，等等。

## #聚焦服务提供者