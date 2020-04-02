---
title: 介绍
---

# 介绍

<a href="https://github.com/hagoxyz"><img src="../imgs/svg/license-MIT-blue.svg" title="license-mit" /></a> <a href="\"><img src="../imgs/svg/build.svg" title="Build status"/></a> <img src="../imgs/svg/downloads.svg" alt="Downloads" />

## Hago是什么

Hago 是一套`渐进式`的`服务提供者框架`。框架为客户端提供多个实现，并把他们从多个实现中解耦出来。服务提供者的改变对它们的客户端是透明的，这样提供了更好的可扩展性。她不仅易于上手，还便于与第三方库或既有项目整合。

- `Hago Core` 是最小可用框架。仅提供最基础的功能，是其他框架开发者作为基础的理想选择。
- `Hago Framework` 以最小可用框架作为基础，提供了常见的基础组件来减少开发者们不必要的工作。
- `Hago For Unity` 在Framework的基础上增加了对Unity的专有组件支持（要求Unity 2017+）。

## Hago的优势

- Hago是渐进式的框架，可以无缝和现有框架融合。无论您的项目处于哪个阶段您都可以轻易的接入Hago。
- Hago提供的依赖注入方案，可以极大程度的帮助项目解耦。
- Hago提供了大量可靠，可持续的公共组件，帮助企业降低开发成本。
- 基于MIT协议，企业可以通过Hago的组件化方案建立私有的公共组件库，提高项目研发效率和质量。
- 轻量级的框架，所有的组件都是可以被移除的，您可以只选择适合您的组件。
- 中文文档完善，极低的学习成本。
- 面向接口编程，底层组件无感知替换。

## 学习路线图

Hago是易于上手的。你只需要有良好的 C# 基础。你就可以非常快速地通过阅读这份 指南 投入开发。

- [服务提供者](architecture/service-provider.html): 了解服务提供者的基本概念，以及系统架构。
- [应用程序](architecture/application.html): 了解核心框架的运行生命周期，以及具备的功能。
- [服务容器](architecture/container.html): 了解核心容器的运行原理以及可用方法。
- [服务门面](architecture/facade.html): 了解服务门面概念，对比常规静态方法。
- [风格指南](style.html): 帮助开发者避免错误，降低沟通成本，解决小纠结和[反模式](anti-pattern.html)。
