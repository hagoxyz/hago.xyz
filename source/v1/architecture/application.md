---
title: 应用程序
---

# 应用程序

`Application`是Hago程序的核心，也是所谓的程序入口。应用程序通过引导来加载服务提供者和其他一些必须的资源。应用程序在一般情况下只允许启动一个，且只能在主线程中启动。

在任何位置，您可以通过`App`全局变量访问应用程序。

## 启动流程

`Application.Bootstrap` -> `Application.Register` -> `Application.Init`

- `Application.Bootstrap` 一般用于引导注册服务提供者，初始配置或者一些其他资源。
- `Application.Register` 用于注册服务提供者到框架。
- `Application.Init` 激活所有服务提供者的`Init函数`，并完成框架初始化。

##### 建议的调用结构：

```markdown
- Application.Bootstrap
- - Application.Register
- - #... more
- Application.Init
```

> 我们一般建议在Bootstrap中调用Register注册函数。
