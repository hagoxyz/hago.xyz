---
title: 事件系统
---

# 事件系统

事件机制是一种很好的应用解耦方式。Hago事件系统让我们可以订阅和监听程序中出现的各种事件。事件系统结合[服务容器](../architecture/container.html)，将提供更加优秀的事件处理方式。

[应用程序](../architecture/application.html)已经默认提供了事件系统，供给全局事件使用。如果您要定义私有范围的事件可以这么做：

``` csharp
var dispatcher = new Dispatcher();
```

## 名词定义

- `载荷`是指程序调用所附带的上下文信息。不同的调用者所提供的上下文信息各不相同。

## 注册普通监听器

通过 `On` 命令您可以注册一个事件的监听器，监听器函数会通过服务容器调用，自动解析并且注入合适的参数。

``` csharp
dispatcher.On("event.name" , (IContainer container)=>{
    //todo
});
```

除了通过Lambda注册外事件监听器外还能够通过对象方法来注册，一共接收3个参数:

- 第一个参数为: 监听的事件名
- 第二个参数为: 事件调用的对象
- 第三个参数为: 事件调用对象的函数名（可选项）

如果您没有传入第三个参数作为函数名，Hago事件系统会通过[字符串方法分析](../helper/str.html#Method)，来分析事件名，并提取出一个函数名，这一特性在有完整的事件名规范时将会大大简化代码。

```csharp
class MyClass
{
    public void CallEvent()
    {
        Console.WriteLine("hello world")
    }
}
```

``` csharp
var cls = new MyClass();
dispatcher.On("MyEvent.CallEvent" , cls); // 分析得出的函数名 : CallEvent
```
