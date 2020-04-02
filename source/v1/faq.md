---
title: 常见问题
---

# 常见问题

本文档描述了开发者经常会遇到的错误，以帮助开发者快速解决问题。

## 依赖注入

- 特性依赖注入总是在构造函数依赖注入之后执行的，请不要在构造函数中使用特性依赖注入的对象。
- 当为一个类注入时出现：`System.MissingMethodException: 没有为该对象定义无参数的构造函数` 请检查构造函数是否是`public`可访问的，只有当构造函数为`public`时才会进行注入。
- `UnresolvableException` 服务未能被解决：
- - 请检查服务提供者是否注册
- - 请检查您是否在`Register`函数中`Make`了服务
- 当注入服务出现`MissingMethodException`异常时，请检查您的构造函数是否是`public`，只有公开的构造函数才能被注入

## 运行时异常

- 编译没有报错，运行时提示`TypeLoadException: Could not load type ...`，有可能是依赖的某模块A进行了升级，导致dll版本有问题，请重新编译依赖了A模块的dll。
