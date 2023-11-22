# SCADA后台服务

## Overview

`SCADA`应用需要编写大量后台服务，以无限循环定时运行的框架为主。这样程序虽然写起来比较简单，但是存在以下几个缺点：

- 如果要求不同的功能以不同的循环周期执行时，不是很方便；
- 循环执行容易受到系统时钟的影响；
- 没有异步处理方案；

  为了解决之前编写后台服务程序的痛点，`SCADA`设计了一个服务程序框架来解决上述问题。简单来说，框架提供了基础的任务类和服务程序类，使用者需要根据自己的实际场景选择合适的任务类，
  并使用服务程序对任务进行调度。当然，任务类和服务程序类都支持自定义扩展。

  首先明确下列概念：

### IOContext

`IOContext`
是一个上下文环境，我们在这个环境里执行时间循环，接收定时器、操作系统以及平台发出的各类事件并进行处理。服务程序运行的各类任务需要在`IOContext`
中进行注册并接受其管理，
`IOContext`就是这些任务的运行环境。

### Timer

`IOContext`需要和定时器配合使用，目前框架提供了两种定时器：

#### SteadyTimer

不会受到操作系统时钟影响的定时器，通常以当时时间为基准加上一个延时参数来进行构造。

#### DeadlineTimer

倒计时定时器，会受到操作系统时钟的影响，通常设置为一个绝对时间。

#### TaskCallback

任务通过执行回调函数来实现具体功能，其形式为：

```C++
    using TaskCallback = std::function<void()>;
```

## Task介绍

用最简单的话来解释，`Task`就是`TaskCallback`与`Timer`的结合体，提供了如下接口供用户调用：

- `start`: 启动任务定时器；
- `execute`: 立即执行任务；
- `activate`: 外部触发执行任务的接口；
- `stop`: 停止任务；
- `restart`: 重启任务；
- `cancel`: 取消任务；
- `update`: 更新任务相关的参数；

`Task`构建出来之后，通过调用`post`函数注册至`IOContext`上归其调度。

目前框架支持的`Task`类型如下：

### OneShotTask

一次性任务，执行完毕后即失效，可指定其执行的具体时间。支持如下两种构造方式：

```C++
/**
 * @brief OneShotTask类的构造函数。
 *
 * 此构造函数创建一个OneShotTask对象。OneShotTask是一个在指定时间执行一次的任务。
 *
 * @param context 提供I/O服务（如套接字，计时器等）的IOContext对象的引用。
 * @param name 表示任务名称的字符串。
 * @param callback 当任务执行时调用的TaskCallback函数。
 * @param execTime 表示应执行任务的时间的DateTime对象。
 */
OneShotTask(IOContext &context, std::string name, 
  TaskCallback callback, const DateTime &execTime)
  
  
/**
   * @brief OneShotTask类的构造函数。
   *
   * 此构造函数创建一个OneShotTask对象。OneShotTask是一个在指定延迟后执行一次的任务。
   *
   * @param context 提供I/O服务（如套接字，计时器等）的IOContext对象的引用。
   * @param name 表示任务名称的字符串。
   * @param callback 当任务执行时调用的TaskCallback函数。
   * @param delay 表示应在多少毫秒后执行任务的延迟时间。
   */
OneShotTask(IOContext &context, std::string name, 
  TaskCallback callback, MillSeconds delay)
```

### PeriodicTask

周期性任务。最为常见的任务类型，可指定其执行周期。周期性任务也可以通过触发方式来执行，两者并不冲突。使用`SteadyTimer`
作为定时器，不受系统时钟影响。其构造方式如下：

```C++
 /**
   * @brief PeriodicTask类的构造函数。
   *
   * 此构造函数创建一个PeriodicTask对象。PeriodicTask是一个周期性执行的任务。
   *
   * @param context 提供I/O服务（如套接字，计时器等）的IOContext对象的引用。
   * @param name 表示任务名称的字符串。
   * @param callback 当任务执行时调用的TaskCallback函数。
   * @param period 表示任务执行的周期（以毫秒为单位）。
   * @param delay 表示在开始执行任务之前应等待的延迟时间（以毫秒为单位，默认为0）。
   */
  PeriodicTask(IOContext &context, std::string name, TaskCallback callback, 
    MillSeconds period, MillSeconds delay = 0)
```

### CronTask

定时任务，以`cron`格式指定定时执行的时间点。使用`DeadLineTimer`作为定时器，受到操作系统时钟影响。其构造方式如下：

```C++
 /**
   * @brief CronTask类的构造函数。
   *
   * 此构造函数创建一个CronTask对象。CronTask是一个根据cron表达式定时执行的任务。
   *
   * @param context 提供I/O服务（如套接字，计时器等）的IOContext对象的引用。
   * @param name 表示任务名称的字符串。
   * @param callback 当任务执行时调用的TaskCallback函数。
   * @param expr 一个cron表达式，用于指定任务的执行时间。
   */
  CronTask(IOContext &context, std::string name, 
    TaskCallback callback, const std::string &expr)

```

`cron`字符串的格式与crontab保持兼容。


## TaskServer介绍

`SCADA`的`TaskServer`是基于最常见的后台服务程序需求(单线程、单IOContext)实现的`Task`服务框架，使用者可以通过继承的方式来实现自己的`Server`。对于有多线程并发处理需求的`Server`，可参考单线程`Server`源码配合自身实际需求来实现。

`TaskServer`已默认订阅数据库装库事件、配置文件变更事件、应用值班状态切换事件。

如此，`SCADA`服务程序的开发过程就分为：
- 根据服务程序的功能定位，选择并实现合适的`Server`；
- 根据服务程序的功能需求，实现各种`Task`；
- 在配置文件里实现对`Task`的参数管理；

`TaskServer`提供的接口待补充。。。