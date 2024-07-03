- [Swift-combine 框架异步编程](#swift-combine-框架异步编程)
  - [1. 前言](#1-前言)
    - [1.1 什么是Combine框架，Combine框架的基本概念](#11-什么是combine框架combine框架的基本概念)
    - [1.2 作为iOS程序员，为什么要学习Combine](#12-作为ios程序员为什么要学习combine)
    - [1.3 Combine框架的核心思想](#13-combine框架的核心思想)
    - [1.4 Combine 的使用场景](#14-combine-的使用场景)
  - [2. 异步编程的概念](#2-异步编程的概念)
    - [2.1 异步和同步概念](#21-异步和同步概念)
    - [2.2 相关程序设计](#22-相关程序设计)
    - [2.3 异步编程的生活场景](#23-异步编程的生活场景)
    - [2.4 Swift开发中的异步场景](#24-swift开发中的异步场景)
    - [2.5 SwiftUI 中异步代码演示实例](#25-swiftui-中异步代码演示实例)
    - [2.6 在程序开发中，如何合理地设计同步和异步功能呢？](#26-在程序开发中如何合理地设计同步和异步功能呢)
    - [2.7 Swift开发中的异步，技术角度：](#27-swift开发中的异步技术角度)
  - [3. 编程方式简介](#3-编程方式简介)
    - [3.1 什么是编程范式(Programming paradigm）](#31-什么是编程范式programming-paradigm)
    - [3.2 常见编程范式](#32-常见编程范式)
  - [4. Combine基本思考](#4-combine基本思考)
    - [4.1 发布者订阅者模式 publish-subscribe pattern](#41-发布者订阅者模式-publish-subscribe-pattern)
    - [4.2 Combine框架概念](#42-combine框架概念)
    - [4.3 发布者(Publishers）](#43-发布者publishers)
    - [4.4 运算符（Qperators）](#44-运算符qperators)
    - [4.5 订阅者（ Subscribers）](#45-订阅者-subscribers)
    - [4.6 订阅（Subscriptions）](#46-订阅subscriptions)
  - [5. Combine 基本演示和处理流程](#5-combine-基本演示和处理流程)
    - [5.1 Operators Map, Filter 进行演示](#51-operators-map-filter-进行演示)
  - [6. Combine 协议讲解](#6-combine-协议讲解)
    - [6.1 **Publisher 协议**：](#61-publisher-协议)
    - [6.2 **Subscriber 协议**：](#62-subscriber-协议)
    - [6.3 **Cancellable 协议**：](#63-cancellable-协议)
    - [6.4 **Subscription 协议**：](#64-subscription-协议)
    - [6.5 **Subscribers.Demand次数配置**](#65-subscribersdemand次数配置)
    - [6.6 **执行上下文**](#66-执行上下文)
    - [6.7 **前置 Swift知识**](#67-前置-swift知识)
  - [7. 结合协议讲解的代码示例](#7-结合协议讲解的代码示例)
    - [7.1 自定义一个简单的订阅者](#71-自定义一个简单的订阅者)
    - [7.2 理解Future发布者的操作](#72-理解future发布者的操作)
    - [7.3 理解Passthrough Subject发布者的操作 以及取消订阅](#73-理解passthrough-subject发布者的操作-以及取消订阅)
    - [7.4 type Erasure 类型抹除](#74-type-erasure-类型抹除)
    - [7.5 自定义订阅者 Custorm Subscriber Sample](#75-自定义订阅者-custorm-subscriber-sample)
    - [7.6 自定义发布者 Future Sample](#76-自定义发布者-future-sample)
    - [7.7 自定义发布者 Subiect Sample](#77-自定义发布者-subiect-sample)
  - [8. 转换操作符Transforming Operators](#8-转换操作符transforming-operators)
    - [8.1 常用操作符 collect, map, flatMap, replace Nil, replaceEmpty, scan](#81-常用操作符-collect-map-flatmap-replace-nil-replaceempty-scan)
    - [8.2 理解map的逻辑转换](#82-理解map的逻辑转换)
    - [8.3 理解flatMap的工作机制](#83-理解flatmap的工作机制)
    - [8.4 理解scan 和reduce的区别](#84-理解scan-和reduce的区别)
  - [9. 过滤操作符 Filtering Operators](#9-过滤操作符-filtering-operators)
    - [9.1 常用的操作符Filtering Operators](#91-常用的操作符filtering-operators)
    - [9.2 理解compactMap的工作机制](#92-理解compactmap的工作机制)
    - [9.3 理解drop 和prefix的untilQutputFrom 参数](#93-理解drop-和prefix的untilqutputfrom-参数)
  - [10. Combine Operators](#10-combine-operators)
    - [10.1 常用的操作符Combine Operators](#101-常用的操作符combine-operators)
    - [10.2 理解switchToLatest的工作机制](#102-理解switchtolatest的工作机制)
    - [10.3 理解combinelatest 和zip的区别](#103-理解combinelatest-和zip的区别)
  - [11. Time Manipulation Operators](#11-time-manipulation-operators)
    - [11.1 获取数据 ，统计数据，统计时间，防抖和超时等等](#111-获取数据-统计数据统计时间防抖和超时等等)
    - [11.2 多个PUblisher之间的关系 ，熟悉发布数据的时间点概念](#112-多个publisher之间的关系-熟悉发布数据的时间点概念)
    - [11.3 理解时间操作的各种模式 ，理解使用场景](#113-理解时间操作的各种模式-理解使用场景)
    - [11.4 理解DispatchQueue.main和 global概念](#114-理解dispatchqueuemain和-global概念)
    - [11.5 理解Thread.sleep概念](#115-理解threadsleep概念)
  - [12. SequenceOperators](#12-sequenceoperators)
    - [12.1 常用的操作符min, max, first, last, output, contains,statisfyAll, reduce](#121-常用的操作符min-max-first-last-output-containsstatisfyall-reduce)
    - [12.2 min:by理解数值比较和逻辑比较的区别](#122-minby理解数值比较和逻辑比较的区别)
    - [12.3 理解Comparable，并且实现这个协议](#123-理解comparable并且实现这个协议)
    - [12.4 理解各个SequenceOperators 的参数，避免没有必要的开销](#124-理解各个sequenceoperators-的参数避免没有必要的开销)
  - [13. Debug](#13-debug)
    - [13.1 常用的DeabuaOperator，print ,print(:to), breakpoint, breakpointOn Error](#131-常用的deabuaoperatorprint-printto-breakpoint-breakpointon-error)
    - [13.2 breakpoint理解各个参数。](#132-breakpoint理解各个参数)
    - [13.3 关于Debug重点，还是在于处理流程的理解，在此基础上进行数据的监控](#133-关于debug重点还是在于处理流程的理解在此基础上进行数据的监控)
  - [14. Error Handling](#14-error-handling)
    - [14.1 常用的ErrorOperator，setFailureType, tryMap, mapError, replace Error, retry](#141-常用的erroroperatorsetfailuretype-trymap-maperror-replace-error-retry)
    - [14.2 mapError, setFailure和retry的工作流程](#142-maperror-setfailure和retry的工作流程)
  - [15. Callback和 Future](#15-callback和-future)
    - [15.1 Swift中闭包closure的定义，以及其特点](#151-swift中闭包closure的定义以及其特点)
    - [15.2 引1用计数【ARC】](#152-引1用计数arc)
    - [15.3 combine中提供的Future](#153-combine中提供的future)
    - [15.4 相同的异步业务，如何用callback和Future实现](#154-相同的异步业务如何用callback和future实现)
    - [15.5 理解callback和Future的实现互相转化](#155-理解callback和future的实现互相转化)
  - [16. Network Layer](#16-network-layer)
    - [16.1 了解和使用 URLSession的data TaskPublisher扩展](#161-了解和使用-urlsession的data-taskpublisher扩展)
  - [17. Key-Value监视和@Published注解](#17-key-value监视和published注解)
    - [17.1 Obiective-C的NSObiect @obic dynamic 属性，也是发布者Publisher](#171-obiective-c的nsobiect-obic-dynamic-属性也是发布者publisher)
    - [17.2 object.publisher(for:,options)参数](#172-objectpublisherforoptions参数)
    - [17.3 Publisher 的扩展 `public func assign<Root>(to kexPath: Reference WritableKeyPath<Root, Self Outputs, on object: Root) -> AnyCancellable`](#173-publisher-的扩展-public-func-assignrootto-kexpath-reference-writablekeypathroot-self-outputs-on-object-root---anycancellable)
    - [17.4 ObservableObject的@Published属性是 Publisher](#174-observableobject的published属性是-publisher)
    - [17.5  Publisher 的扩展`public func assign(to published: inout Published<Self Output>.Publisher).`](#175--publisher-的扩展public-func-assignto-published-inout-publishedself-outputpublisher)
    - [17.6 熟悉Key-Valve 监视的接口后，可以很方便地应用的项目中](#176-熟悉key-valve-监视的接口后可以很方便地应用的项目中)
  - [18. 并发编程概念回顾](#18-并发编程概念回顾)
    - [18.1 iOS中多线程概念和用语。](#181-ios中多线程概念和用语)
    - [18.2 队列DispatchQueue优先级。](#182-队列dispatchqueue优先级)
    - [18.3 信号量semaphore的工作流程和使用示例](#183-信号量semaphore的工作流程和使用示例)
    - [18.4 同步和异步 在DispatchQueve 的执行](#184-同步和异步-在dispatchqueve-的执行)
  - [19. Share和Multicast Operators](#19-share和multicast-operators)
    - [19.1 publisher的receive data的次数](#191-publisher的receive-data的次数)
    - [19.2 share Operator](#192-share-operator)
    - [19.3 make Connectable Operator](#193-make-connectable-operator)
    - [19.4 multicast(subject) operator](#194-multicastsubject-operator)
  - [20. Scheduler](#20-scheduler)
    - [20.1 Scheduler的概念](#201-scheduler的概念)
    - [20.2 各种Scheduler](#202-各种scheduler)
    - [20.3 Combine使用切换上游和下游的执行上下文](#203-combine使用切换上游和下游的执行上下文)
    - [20.4 subscribe(on)和receive(on)的接口定义](#204-subscribeon和receiveon的接口定义)
  - [21 自定义订阅者Subscribers和Subscribers.Demand](#21-自定义订阅者subscribers和subscribersdemand)
    - [21.1 认识为什么需要自定义订阅者（Subscriber）](#211-认识为什么需要自定义订阅者subscriber)
    - [21.2 复习Subscriber 协议](#212-复习subscriber-协议)
    - [21.4 Subscriber协议和订阅机制，自定义Subscriber](#214-subscriber协议和订阅机制自定义subscriber)
    - [21.5 使用结构体struct或类Cilass实现 Subscriber协议的不同](#215-使用结构体struct或类cilass实现-subscriber协议的不同)
  - [22. 自定义 发布者Publisher和订阅Subsctription](#22-自定义-发布者publisher和订阅subsctription)
    - [22.1 认识为什么需要自定义发布者（Publisher）和订阅(Subseription)](#221-认识为什么需要自定义发布者publisher和订阅subseription)
    - [22.2 如何扩展发布者Publisher](#222-如何扩展发布者publisher)
    - [22.3 发布者Publisher和订阅Subseription的自定义实现](#223-发布者publisher和订阅subseription的自定义实现)
    - [22.4 Publisher缓存机制的设计](#224-publisher缓存机制的设计)
    - [22.5 如何定义Operator，也就是有上游（Upstream）发布者](#225-如何定义operator也就是有上游upstream发布者)
    - [22.6 灵活使用中转订阅者 Sink](#226-灵活使用中转订阅者-sink)
  - [23. Backpressure概念以及对应方法](#23-backpressure概念以及对应方法)
    - [23.1 Subscriber的订阅对象重启方法](#231-subscriber的订阅对象重启方法)
    - [23.2 Subscribeis.Demnand的使用](#232-subscribeisdemnand的使用)
    - [23.3 Publisher的声明式sink定义](#233-publisher的声明式sink定义)
    - [23.4 Subscribers.Demand关于 backpressure 的处理流程设计](#234-subscribersdemand关于-backpressure-的处理流程设计)


# Swift-combine 框架异步编程

## 1. 前言

### 1.1 什么是Combine框架，Combine框架的基本概念

> 官网地址： https:/developer.apple.com/documentation/combine

Combine框架是苹果公司在iOS 13及更高版本中引入的一个强大的响应式编程框架。它的主要目的是简化异步数据流的处理和处理多个数据源之间的交互。Combine提供了一种声明性的方法来处理数据流，允许你在数据流的各个环节执行操作、组合数据和管理数据流的生命周期。

以下是Combine框架的一些基本概念：

1. Publisher（发布者）：发布者是Combine框架中的核心组件，用于生成和发送数据流。它可以是一个单一值、一系列值或一个错误。常见的发布者包括`Just`、`Future`、`Timer`和`URLSession`。

2. Subscriber（订阅者）：订阅者订阅发布者，接收发布者发送的数据流，并对数据进行处理。它定义了数据接收、完成和错误处理的逻辑。你可以使用`sink`操作符创建一个订阅者。

3. Operator（操作符）：Combine提供了一系列操作符，用于对数据流进行转换、筛选和组合。这些操作符允许你声明式地对数据流进行处理，而不需要编写大量的回调函数。

4. Cancellable（可取消对象）：订阅一个数据流将返回一个可取消对象，允许你随时取消订阅，以停止接收数据。

5. Subject（主题）：主题是一个特殊类型的发布者，可以动态生成数据并将其发送给订阅者。有`PassthroughSubject`和`CurrentValueSubject`两种常见类型的主题。




### 1.2 作为iOS程序员，为什么要学习Combine

1. 现代化编程范式：Combine是一种响应式编程框架，它可以帮助iOS开发人员更轻松地处理异步数据流和事件。这是一种现代化的编程范式，有助于编写更清晰、可维护和高效的代码。

2. 集成性：Combine与苹果的其他框架和API（如UIKit、SwiftUI、Core Data和网络请求）无缝集成。它可以用于处理各种iOS应用程序中的数据流，包括用户界面更新、网络请求、数据库操作等。

3. 减少回调地狱：Combine减少了回调嵌套的问题，使异步代码更易于理解和维护。你可以使用操作符来连接和转换数据流，而不必编写复杂的嵌套回调。

4. 多线程处理：Combine提供了处理多线程和并发操作的工具，使你能够轻松地在后台线程中执行任务，并在主线程上更新用户界面。

5. 强类型：Combine是Swift语言的一部分，因此它与Swift的类型系统无缝协作，提供了类型安全的编程体验。


总的来说，学习Combine框架可以提高iOS开发人员的编程技能，使他们能够更好地处理异步任务和数据流，提高应用程序的性能和可维护性。从节约时间的观点来看，熟悉Combine框架 ，可以让您更加关注业务的设计，从复杂的异步事件处理中解放出来。

### 1.3 Combine框架的核心思想

Combine框架的核心思想是响应式编程（Reactive Programming）。响应式编程是一种编程范式，旨在处理数据流和异步事件，使程序更具响应性和可维护性。Combine框架引入了以下核心思想：

1. 数据流：Combine将数据视为一系列事件或值的流，而不仅仅是单一的静态值。这些事件可以是用户输入、网络响应、传感器数据等，它们以时间顺序的方式到达应用程序。

2. 声明性：Combine鼓励以声明性的方式描述数据流的操作和变换。你可以使用操作符来定义数据流的处理逻辑，而不是编写大量的回调函数。

3. 异步性：Combine适用于异步操作，它允许你轻松地处理异步任务，如网络请求、文件读写和定时器。数据流可以在后台线程上生成和处理，同时支持切换到主线程以更新用户界面。

4. 订阅机制：Combine引入了发布者-订阅者模型，其中发布者生成数据并将其发送给订阅者。订阅者定义了如何处理数据流，包括数据接收、错误处理和完成事件。订阅者可以随时取消订阅，以停止接收数据。

5. 组合操作符：Combine提供了丰富的操作符，用于组合、过滤、映射和转换数据流。这些操作符使你能够以清晰、紧凑的方式构建复杂的数据流处理逻辑。

6. 错误处理：Combine提供了强大的错误处理机制，允许你处理和传播错误。这有助于编写健壮的应用程序，能够适应各种异常情况。

7. 多线程和并发：Combine支持多线程和并发操作，使你可以方便地将任务分发到不同的线程，并在需要时切换到主线程以进行UI更新。

总的来说，Combine的核心思想是以数据流为中心，通过声明性的方式处理异步事件和数据，提供了强大的工具和模型来简化和优化iOS应用程序的编写。这有助于提高代码的可读性、可维护性和性能。




### 1.4 Combine 的使用场景

Combine框架可以应用于多种场景，特别适用于处理异步数据流、事件驱动编程和数据响应的情况。以下是一些Combine的试用场景：

1. 网络请求：Combine可用于处理网络请求，从服务器获取数据，并以响应式方式处理和显示数据。你可以使用Combine的操作符和Publisher来处理网络请求的结果、错误和超时。

2. 用户界面更新：Combine使你能够轻松地将数据绑定到用户界面元素，以实现数据的实时更新。这在SwiftUI应用程序中特别有用，因为SwiftUI本身也支持Combine。

3. 用户输入处理：Combine可以用于处理用户输入，如文本字段的文本变化、按钮点击和手势识别。你可以创建数据流，以响应用户的交互操作。

4. 数据转换和映射：Combine提供了各种操作符，用于在数据流中进行转换、映射和过滤操作。这对于将数据从一种格式转换为另一种格式非常有用。

5. 定时器和延迟操作：Combine允许你创建定时器和延迟操作，以在一段时间后执行某些任务。这对于实现动画和计时器非常有用。

6. 多个数据源的协同操作：当你需要合并多个数据源（例如，从不同的API端点获取数据）或根据多个数据源的状态执行操作时，Combine可以帮助你处理这种情况。

7. 错误处理：Combine提供了丰富的错误处理机制，允许你处理和传播错误。这对于构建健壮的应用程序非常重要。

8. 数据缓存和持久化：你可以使用Combine来管理数据的缓存和持久化，确保数据在内存和存储之间同步。

9. 传感器数据：如果你的应用程序需要处理传感器数据，如位置、陀螺仪或加速度计，Combine可以用于创建数据流来实时处理这些数据。

10. 用户交互和响应：当用户在应用中执行操作时，例如刷新天气数据、切换城市或设置偏好，Combine可以用于响应这些用户交互事件，以更新数据流和界面。

11. 自定义数据流管理：Combine允许你创建自定义的发布者和订阅者，以适应特定的应用场景。

总的来说，Combine适用于许多不同的iOS和macOS应用程序场景，特别是在需要处理异步任务、数据响应和事件驱动编程时，它可以大大简化代码编写，提高应用程序的性能和可维护性。




以下是一个简单的Combine代码示例，演示了如何创建一个数据流、使用操作符进行变换和最终订阅数据流。这个示例将一个整数数组中的元素加倍，然后过滤出其中的偶数。注意，这个示例使用Swift Playground来展示Combine的基本用法：

```swift
import Combine

// 创建一个整数数组发布者
let numbersPublisher = [1, 2, 3, 4, 5].publisher

// 使用map操作符将数组中的每个元素加倍
let doubledNumbersPublisher = numbersPublisher
    .map { $0 * 2 }

// 使用filter操作符筛选出偶数
let evenNumbersPublisher = doubledNumbersPublisher
    .filter { $0 % 2 == 0 }

// 订阅数据流，接收并处理结果
let subscription = evenNumbersPublisher.sink { value in
    print(value)
}

// 在订阅之后的某个时刻取消订阅
subscription.cancel()
```

这个示例中，我们首先创建了一个整数数组发布者(`numbersPublisher`)，然后使用`map`操作符将每个元素都加倍，再使用`filter`操作符筛选出偶数。最后，我们使用`sink`操作符来订阅数据流，并在订阅中打印出偶数值。

请注意，Combine的`sink`操作符返回一个`Cancellable`对象，你可以使用它来取消订阅数据流，以停止接收事件。在示例的最后，我们演示了如何取消订阅。

这只是Combine的一个非常简单的示例，但它展示了创建、变换和订阅数据流的基本步骤。在实际应用中，你可以使用Combine来处理更复杂的异步任务和数据流，以提高代码的可读性和可维护性。


---


## 2. 异步编程的概念

### 2.1 异步和同步概念

异步和同步是两种不同的程序执行模式，涉及到如何处理和控制任务的执行顺序和时间。以下是它们的基本概念：

**同步（Synchronous）**：

1. **阻塞式执行**：在同步操作中，任务按照它们的出现顺序依次执行，一个任务完成后才会开始下一个任务。如果一个任务需要一些时间来完成，整个程序将被阻塞，等待该任务完成。

2. **顺序性**：同步操作通常是按照程序的顺序依次执行的，任务之间是串行的。这使得代码易于理解，因为你可以确保在处理某个任务之前，前一个任务已经完成。

3. **示例**：在同步文件读取操作中，程序将读取文件的内容，直到读取完成之前，程序会一直等待。

**异步（Asynchronous）**：

1. **非阻塞式执行**：在异步操作中，任务不会阻塞程序的执行，而是在后台执行。程序可以继续执行其他任务，而不必等待异步任务完成。

2. **并行性**：异步操作可以并行执行，这意味着多个任务可以同时运行，而不必等待其他任务完成。这可以提高程序的性能和响应性。

3. **回调或通知机制**：异步操作通常涉及回调函数、代理或通知机制，用于在异步任务完成时通知程序。程序可以继续执行其他任务，然后在异步任务完成时执行回调函数。

4. **示例**：在异步网络请求中，应用程序可以继续响应用户操作，而不必等待网络请求完成。当请求完成时，回调函数将被调用，以处理接收到的数据。

异步编程通常用于处理需要较长时间的操作，如网络请求、文件读写、用户界面更新和传感器数据等。它可以提高应用程序的响应性，防止应用程序在等待某些任务完成时被冻结。然而，异步编程可能会引入一些复杂性，因为你需要处理任务的并发性和顺序性。 Combine框架是一种用于简化和处理异步编程的工具，它提供了声明式的方式来处理异步数据流和事件。




### 2.2 相关程序设计

相关程序设计（Reactive Programming）是一种编程范式，旨在处理数据流和事件驱动编程。它强调在应用程序中的数据流和数据变化之间建立响应式关系，使程序能够更好地应对异步事件和数据流的需求。相关程序设计通常与响应式框架（如RxSwift、ReactiveX、Combine等）一起使用，这些框架提供了工具和模型来实现相关编程。

以下是与相关程序设计相关的一些关键概念和原则：

1. **数据流**：相关编程的核心思想是将数据视为事件流或数据流。这些事件可以是用户输入、传感器数据、网络请求的响应等。编程重点是如何有效地处理和响应这些事件。

2. **响应性**：程序应该能够快速响应事件和数据的变化。相关编程鼓励通过响应式操作来处理数据流，以确保程序具有高度的响应性和实时性。

3. **声明性**：相关编程强调声明性代码，即通过描述要执行的操作来实现目标，而不是详细指导计算机如何执行。这使代码更易理解和维护。

4. **观察者模式**：在相关编程中，通常使用观察者模式。数据的生产者（称为"可观察对象"）生成事件并通知已注册的观察者（"订阅者"）来处理这些事件。

5. **数据变换和过滤**：相关编程提供操作符来转换、过滤和组合数据流。这些操作符使数据的处理变得更容易和高效。

6. **异步编程**：因为许多事件和数据流是异步的，所以相关编程通常用于处理异步编程。它提供了工具来管理异步任务和事件。

7. **错误处理**：处理错误和异常情况也是相关编程的一部分。它提供了机制来处理和传播错误，以确保程序能够适应各种异常情况。

8. **可组合性**：相关编程允许将操作符和数据流组合在一起，以构建更复杂的数据流处理逻辑。这提高了代码的可组合性和可重用性。

9. **多平台支持**：许多相关编程框架支持多种平台，包括iOS、Android、Web和桌面应用程序。这使得在不同平台上共享相关的代码和概念变得更容易。

相关程序设计和相关框架的目标是使应用程序更具响应性、可维护性和性能。它特别适用于需要处理数据流和异步事件的应用程序，例如移动应用程序、网络服务、游戏开发和传感器数据处理。这个编程范式已经成为现代软件开发中的一个重要工具。




### 2.3 异步编程的生活场景

异步编程在日常生活中有许多实际场景，涵盖了从计算机编程到日常任务的各种情况。以下是一些示例：

1. **网络通信**：网络通信是异步编程的典型示例。当你使用Web浏览器加载网页、发送电子邮件、下载文件或使用社交媒体应用时，都会进行网络请求和响应。这些请求是异步的，因为它们需要等待数据的传输。

2. **多任务操作系统**：操作系统通常需要同时运行多个任务，这些任务可以是应用程序、后台服务或用户界面元素。这些任务的调度和执行是异步的，操作系统负责协调它们的执行。

3. **手机应用**：在手机应用中，你经常与异步编程交互。例如，当你使用社交媒体应用时，你可以同时接收消息、通知和新帖子。这些事件是异步的，应用程序需要及时响应它们。

4. **电子邮件和通讯**：发送和接收电子邮件是异步过程。你可以编写电子邮件，但它不会立即被收件人接收。邮件服务器负责异步传递邮件。

5. **在线购物**：当你购物时，将商品添加到购物车、进行结账和支付都是异步操作。支付可以需要等待银行批准交易，而在此期间你可以继续浏览其他商品。

6. **社交媒体互动**：在社交媒体平台上，你可以发布帖子、评论、点赞和分享。这些互动是异步的，其他用户可以在不同的时间点对它们进行回应。

7. **家居自动化**：智能家居系统使用异步编程来处理各种任务，如控制灯光、温度、安全系统和家电。你可以通过智能手机应用远程控制这些系统，它们需要异步通信来执行你的指令。

8. **在线游戏**：在线游戏通常涉及多个玩家，他们可以在不同地点和不同时间点参与游戏。游戏引擎必须异步处理多个玩家的输入和状态更新。

9. **机器学习和大数据分析**：在机器学习和大数据分析中，处理大量数据和训练模型是异步操作。这些任务可能需要很长时间来完成。

10. **天气预报**：天气数据的收集和更新是异步的，而用户需要随时获取最新的天气信息。

这些是异步编程在生活中的一些常见示例，强调了异步操作是现代计算和通信的重要组成部分。异步编程允许系统和应用程序在处理多个任务和事件时更加高效和灵活。




### 2.4 Swift开发中的异步场景

在Swift开发中，有许多异步场景，其中一些包括：

1. **网络请求**：当你从网络获取数据时，通常需要进行异步网络请求。例如，使用`URLSession`或网络框架（如Alamofire）发起HTTP请求，然后在响应返回后处理数据。这确保应用程序不会被网络延迟阻塞。

2. **用户界面更新**：在iOS应用程序中，你经常需要在用户界面上异步更新数据，以响应用户操作或后台任务的完成。例如，在后台线程中加载图像并在主线程上更新UI。

3. **数据持久化**：读取或写入磁盘上的文件（如读取本地数据库或写入文件）通常需要异步操作，以避免阻塞应用程序。

4. **并发任务**：在多核CPU上，你可以使用多线程来执行任务，以提高性能。Swift的`DispatchQueue`和GCD（Grand Central Dispatch）是一种强大的方式来进行并发编程。

5. **定时任务**：需要定期执行的任务，如轮询服务器以获取更新或执行定时器任务，都是异步的。你可以使用GCD或计时器来实现这些功能。

6. **用户输入和事件处理**：当用户与应用程序交互时，需要异步处理用户输入和事件。例如，点击按钮、触摸屏幕或旋转设备会触发异步事件，应用程序必须处理这些事件。

7. **后台任务**：执行后台任务，如在后台下载数据、处理通知或更新数据，是一种异步场景。这可确保应用程序在后台执行任务时仍然能够响应用户的操作。

8. **传感器数据**：处理传感器数据，如GPS位置、陀螺仪、加速度计等，通常是异步操作，因为这些数据在不断变化。

9. **长时间运行的操作**：某些操作可能需要较长时间来完成，例如图像处理、数据分析或机器学习任务。这些操作通常需要在后台线程上运行，以防止阻塞主线程。

10. **多任务操作系统**：操作系统本身是一个异步操作系统，可以同时运行多个任务和进程，它们之间可以并行执行。

Swift提供了强大的工具来处理这些异步场景，包括`async/await`（Swift 5.5及更高版本）、`DispatchQueue`（GCD）、`URLSession`、Combine框架、异步函数等。这些工具使异步编程更容易管理，并提供了更高的性能和响应性。




### 2.5 SwiftUI 中异步代码演示实例

在SwiftUI中执行异步操作的示例是获取并显示从网络获取的数据。以下是一个简单的示例，演示如何在SwiftUI中使用异步函数来获取数据并将其显示在用户界面上。这个示例使用Swift 5.5中引入的`async/await`语法。

```swift
import SwiftUI

@main
struct AsyncExampleApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}

struct ContentView: View {
    @State private var data: String = "Loading..."
    
    var body: some View {
        VStack {
            Text(data)
                .padding()
                .onAppear {
                    Task {
                        do {
                            // 使用异步函数获取数据
                            let result = try await fetchData()
                            data = result
                        } catch {
                            data = "Error: \(error.localizedDescription)"
                        }
                    }
                }
        }
    }
    
    func fetchData() async throws -> String {
        // 模拟网络请求或异步操作
        await Task.sleep(2 * 1_000_000_000) // 模拟2秒延迟
        return "Data from the network"
    }
}
```

在这个示例中，我们创建了一个简单的SwiftUI应用，包含一个`ContentView`，其中的文本显示了数据。在`onAppear`闭包中，我们使用`Task`来执行异步函数`fetchData`，该函数模拟了一个网络请求，等待2秒后返回数据。异步操作的结果在`data`属性中更新，这将自动刷新UI。

这是一个非常基本的示例，但它演示了如何在SwiftUI中使用`async/await`来执行异步操作，并如何在UI上更新数据。在实际应用中，你可以替换`fetchData`函数来进行真正的网络请求和数据处理。




### 2.6 在程序开发中，如何合理地设计同步和异步功能呢？

在程序开发中，合理设计同步和异步功能是非常重要的，因为这有助于确保程序的性能、可维护性和用户体验。以下是一些关于如何合理设计同步和异步功能的建议：

**1. 了解任务的性质：** 首先，要清楚任务的性质。某些任务天然是同步的，例如基本的数学运算。其他任务可能需要异步执行，例如网络请求或文件读写。了解任务的性质有助于确定何时使用同步和异步方法。

**2. 避免主线程阻塞：** 主线程应保持响应，避免长时间运行的任务阻塞主线程。长时间运行的任务应该在后台线程上执行，以确保用户界面的流畅性。

**3. 使用异步来提高性能：** 异步编程可用于提高程序性能。例如，可以使用异步加载图像，以便在加载图像时应用程序仍然响应用户操作。

**4. 错误处理：** 在异步任务中，错误处理非常重要。确保在异步操作中进行适当的错误处理，以处理网络错误、文件不存在等情况。

**5. 可取消性：** 如果可能，确保异步任务是可取消的。这允许用户或程序在需要时取消任务，以避免不必要的工作。

**6. 并发性：** 考虑并发任务的需求。某些任务可能需要并行执行，而其他任务可能需要按顺序执行。选择适当的工具（如GCD）来管理并发任务。

**7. 使用合适的工具和框架：** 针对不同的任务，使用适当的工具和框架。Swift提供了`async/await`来处理异步任务，GCD用于并发编程，Combine用于响应式编程。

**8. 可测试性：** 设计代码时考虑测试性，使得同步和异步功能可以轻松测试。这将有助于及早发现和修复问题。

**9. 优化用户体验：** 异步任务应在后台运行，以优化用户体验。例如，可以在后台下载数据，以确保用户不必等待。

**10. 安全性：** 考虑数据访问的线程安全性。在多线程环境中，确保共享数据的安全访问是至关重要的。

在设计上，同步、异步和批处理之间的关系不是对立的，是一个互相补充且相融的设计，目标是在业务逻辑上没有 “缺口”， 并且让用户体验上不受影响。

同步的功能中，可以有异步调用，异步功能里可以有同步处理，也可以触发一定的事件，让批处理进行。

最重要的是，合理的设计需要根据具体的需求和上下文来进行。不同的应用程序和情况可能需要不同的同步和异步策略。因此，了解任务性质，考虑性能、用户体验、错误处理和可测试性等因素，以及选择适当的工具，都是合理设计同步和异步功能的关键。




### 2.7 Swift开发中的异步，技术角度：

```
通知中心-NotificationCenter
代理-Delegates
计时器-Timers
多线程-Operations ( high level)
多线程-GrandCentralDispatch (low level)
回调-ClosureCallBacks
```



1. **async/await**：Swift 5.5引入;
2. **GCD（Grand Central Dispatch）**：
3. **Operation和OperationQueue**：
4. **Combine框架**：
5. **网络库和API**：
6. **异步操作队列**：
7. **SwiftUI中的异步**：
8. **第三方库和框架**：


你提到的这些是在iOS开发中常用的处理异步和事件驱动编程的技术和模式。让我简要解释一下它们的作用：

1. **通知中心 (NotificationCenter)**：通知中心是iOS中的一种发布-订阅机制，允许不同部分的代码通信，而不需要直接引用或了解彼此。一个对象可以发布通知，而其他对象可以订阅这些通知，并在特定事件发生时接收通知。通知中心用于应用内事件的广播和响应，例如键盘出现/消失、设备旋转等。

2. **代理 (Delegates)**：代理是一种设计模式，它允许一个对象委托另一个对象来执行特定的任务。在iOS开发中，通常用于视图控制器和视图之间的通信，以及其他对象之间的协作。代理允许对象通知其代理对象有关其状态或事件的更改。

3. **计时器 (Timers)**：计时器允许你执行代码在预定的时间间隔内重复或延迟执行。在iOS中，你可以使用`Timer`类创建计时器，用于执行后台任务、周期性刷新用户界面或处理定时事件。

4. **多线程 (Operations)**：`Operation`和`OperationQueue`是用于多线程编程的高级抽象，允许你在应用程序中并发执行任务。`Operation`是表示单个任务的抽象，而`OperationQueue`管理操作的并发性和调度。这用于处理大型并行任务，如后台下载、图像处理等。

5. **多线程 (Grand Central Dispatch, GCD)**：GCD是iOS中的底层并发和并行编程技术，它提供了强大的API，允许你管理线程、队列、同步和异步任务。GCD用于实现任务的并发执行，提高性能，例如在后台执行任务，以确保主线程的响应性。

6. **回调 (Closure Callbacks)**：回调是一种常见的模式，允许你将一个函数传递给另一个函数，以在特定事件发生时调用。在Swift中，回调通常使用闭包来实现。回调用于异步操作的结果通知，例如网络请求完成、数据加载完成等。

这些技术和模式都是在iOS开发中非常有用的，它们可以帮助你管理异步操作、事件处理和多线程任务。选择适当的技术和模式取决于你的具体需求和应用程序架构。




在Swift开发中，处理异步操作是至关重要的，因为许多任务，特别是与网络通信、文件读写、用户界面更新和后台任务等有关，都是异步的。以下是一些在技术角度上处理异步操作的方法和工具：

1. **async/await**：Swift 5.5引入了`async/await`语法，使编写异步代码变得更容易。通过标记函数为`async`，你可以创建异步函数，然后在函数内使用`await`来等待异步任务完成。这可以大大简化异步代码的编写和理解。

2. **GCD（Grand Central Dispatch）**：GCD是用于多线程和并发编程的强大工具。你可以使用`DispatchQueue`来创建队列，将任务提交给队列以异步执行，管理任务的并发性，以及确保线程安全。

```swift
// 异步任务
DispatchQueue.global().async {
    // 在后台线程执行任务
    DispatchQueue.main.async {
        // 切换到主线程更新UI
    }
}
```

3. **Operation和OperationQueue**：`Operation`和`OperationQueue`是GCD的高级抽象，用于管理并发任务。它们允许你创建自定义操作并将它们添加到队列中以异步执行。

```swift
let operationQueue = OperationQueue()
operationQueue.addOperation {
    // 异步任务
}
```

4. **Combine框架**：Combine是苹果引入的用于处理异步事件流的框架。它提供了丰富的操作符，可用于处理和转换数据流、执行异步任务、错误处理等。特别适用于响应式编程。

5. **网络库和API**：在Swift开发中，你通常会使用网络库（如`URLSession`）来执行异步网络请求。这些库提供了用于创建和管理网络请求的API，通常包括异步回调或`async/await`支持。

```swift
URLSession.shared.dataTask(with: url) { data, response, error in
    // 处理网络响应（异步回调）
}.resume()
```

6. **异步操作队列**：你可以使用`OperationQueue`或`DispatchQueue`来创建自定义队列，以管理异步操作的顺序和优先级。

```swift
let customQueue = DispatchQueue(label: "com.example.myqueue")
customQueue.async {
    // 异步任务
}
```

7. **SwiftUI中的异步**：SwiftUI支持异步操作，你可以使用异步函数来处理异步操作并将数据绑定到视图以实现响应性。例如，使用`Task`来执行异步操作，然后更新视图。

```swift
Task {
    let data = try await fetchData()
    self.data = data
}
```

8. **第三方库和框架**：除了Swift原生的工具和框架，还有许多第三方库和框架可以用于异步操作，例如Alamofire、PromiseKit、RxSwift等。

合理处理异步操作是Swift开发中的关键部分，可以提高性能、响应性和用户体验。选择适当的工具和技术，根据应用程序的需求来进行设计和实施异步功能。





## 3. 编程方式简介

### 3.1 什么是编程范式(Programming paradigm）

编程范式（Programming Paradigm）是一种编程方法或思维方式，它定义了如何组织和结构化计算机程序。编程范式是一种编程的哲学或理念，规定了在解决问题时应该使用什么样的概念、原则和模式。不同的编程范式强调不同的思维方式和方法，以达到编写高效、可维护和可理解的代码的目标。

### 3.2 常见编程范式

下面是一些常见的编程范式：

1. **命令式编程（Imperative Programming）**：这是一种基于指令和状态的编程范式，重点是通过一系列的命令来改变程序的状态。常见的编程语言如C、C++和Java属于这一范式。

2. **函数式编程（Functional Programming）**：函数式编程将计算视为数学函数的应用，避免可变状态和共享状态。它强调不可变性、纯函数、高阶函数和递归。编程语言如Haskell、Lisp和Scala支持函数式编程。

3. **面向对象编程（Object-Oriented Programming，OOP）**：面向对象编程以对象为中心，将数据和操作封装在对象中，强调类、继承、封装和多态。编程语言如Java、Python和C#支持OOP。

4. **逻辑编程（Logic Programming）**：逻辑编程使用逻辑规则和推理来解决问题，通常使用规则和查询来描述问题和解决方案。Prolog是一种逻辑编程语言的例子。

5. **并发编程（Concurrent Programming）**：并发编程强调多个任务的同时执行，通常使用线程、进程和协程来实现并发。编程语言如Go和Erlang专门设计用于并发编程。

6. **声明式编程（Declarative Programming）**：声明式编程强调“做什么”，而不是“如何做”。SQL和HTML是声明式编程的例子，其中你描述了你想要的结果，而不需要编写详细的操作步骤。

7. **泛型编程（Generic Programming）**：泛型编程允许编写通用代码，而不考虑特定的数据类型。C++的模板是泛型编程的一个示例。

8. **反应式编程（Reactive Programming）**：反应式编程使用数据流和事件流来建模问题，强调事件驱动和响应性。RxJava和RxSwift是反应式编程的示例。

9. **模式匹配编程（Pattern Matching Programming）**：模式匹配编程强调根据输入的模式匹配来选择不同的处理逻辑。它在函数式编程语言中非常常见。

10. **元编程（Metaprogramming）**：元编程允许程序自身编写或修改自身的代码，通常用于生成代码、代码分析和自定义领域特定语言（DSL）。

不同的编程范式适合不同类型的问题和应用程序，以及不同的开发者风格。现代编程语言和框架通常支持多种编程范式的组合，允许开发者选择最合适的工具来解决问题。选择适合你的问题和项目的编程范式可以提高代码的质量和可维护性。

3.3 Combine框架的编程范式

Combine框架是一个现代的响应式编程框架，它结合了多种编程范式，包括以下几种：

1. **响应式编程（Reactive Programming）**：Combine的核心思想是响应式编程，它强调数据流和事件流的处理。使用Combine，你可以创建数据流、将数据流转换、筛选、合并和订阅数据流的事件。这种编程范式使得处理异步事件和数据流变得更加容易和高效。

2. **函数式编程（Functional Programming）**：Combine借鉴了函数式编程的一些思想，例如使用高阶函数（Higher-Order Functions）来处理数据流、将操作符应用于数据流的元素以及使用纯函数来进行数据变换。这有助于确保数据流的可预测性和不可变性。

3. **声明式编程（Declarative Programming）**：Combine强调的是声明式编程，其中你描述要执行的操作和数据流的操作，而不需要编写详细的步骤。这使得代码更易于理解和维护。

4. **异步编程（Asynchronous Programming）**：由于Combine处理的通常是异步事件和数据流，它强调了异步编程。使用Combine，你可以处理异步操作，例如网络请求、定时器、用户输入等。

5. **链式编程（Fluent Interface）**：Combine支持链式编程，你可以通过连接操作符和方法来构建数据流处理管道，从而实现可读性强的代码。这种链式编程风格有助于清晰表达数据流的处理流程。

6. **响应式设计模式（Reactive Design Patterns）**：Combine框架在一定程度上遵循了响应式设计模式，例如观察者模式、订阅者模式和责任链模式。这些设计模式有助于解决数据流的订阅和分发。

Combine框架的综合使用这些编程范式，使得它成为处理异步事件和数据流的强大工具。它适用于多种应用场景，包括iOS和macOS应用程序开发、网络编程、用户界面更新和大规模数据流处理。借助Combine，开发者可以更容易地构建具有高度响应性和可维护性的应用程序。






## 4. Combine基本思考


### 4.1 发布者订阅者模式 publish-subscribe pattern




发布者-订阅者模式（Publish-Subscribe Pattern）是一种设计模式，用于实现组件之间的松散耦合。在这个模式中，有两种角色：发布者（Publisher）和订阅者（Subscriber）。发布者负责发布事件或消息，而订阅者订阅或监听感兴趣的事件或消息。当发布者发布一个事件时，所有订阅该事件的订阅者都会收到通知并执行相应的操作。

以下是发布者-订阅者模式的关键特点和组成部分：

1. **发布者（Publisher）**：发布者是负责发布事件或消息的组件。它维护一个事件队列或主题，当事件发生时，发布者将通知所有订阅了该事件的订阅者。发布者通常提供一种机制来让订阅者订阅和取消订阅事件。

2. **订阅者（Subscriber）**：订阅者是感兴趣并订阅发布者发布的事件或消息的组件。它通过订阅特定的事件来表达兴趣。当事件发生时，订阅者会接收到通知，并执行与事件相关的操作。

3. **事件/消息**：事件是发布者发布的通知，可能携带一些数据。事件可以有不同的类型和属性，根据应用程序的需求定义。

4. **事件队列/主题**：发布者通常维护一个事件队列或主题列表，用于存储和管理待发布的事件。订阅者可以选择订阅特定的事件队列或主题。

5. **通知/回调**：发布者通常使用回调函数、观察者模式或事件总线等方式来通知订阅者有关事件的发生。这可以是同步或异步通知，取决于实现方式。

6. **松散耦合**：发布者-订阅者模式实现了松散耦合，因为发布者和订阅者之间没有直接的依赖关系。发布者不需要知道订阅者的详细信息，只需发布事件，而订阅者只需订阅感兴趣的事件。

发布者-订阅者模式常用于各种软件应用中，包括图形用户界面框架、消息队列系统、事件驱动编程等。它提供了一种有效的方式来处理异步通信和多组件之间的协作。这个模式的一个典型应用是在图形用户界面开发中，用于处理用户交互事件的通知和处理。



### 4.2 Combine框架概念

在 Combine 框架中，有几个重要的概念，包括 Publisher、Subscriber、Operator 和 Subscription。以下是每个概念中需要注意的关键点：

1. **Publisher（发布者）**：

   - **发布数据流**：Publisher 是一个可以发布数据流的类型，它可以发出值、完成事件或错误事件。
   - **背压处理**：Publisher 可以处理背压（backpressure），它会适应订阅者的速度，以避免数据丢失或缓冲区溢出。
   - **多值发出**：Publisher 可以发出多个值，例如使用 `map` 和 `flatMap` 操作符。
   - **错误处理**：Publisher 可以发出错误事件，需要使用 `catch` 和 `retry` 操作符来处理错误。

2. **Subscriber（订阅者）**：

   - **订阅数据流**：Subscriber 订阅 Publisher，以接收其发出的事件。Subscriber 通过 `sink` 方法来订阅 Publisher。
   - **处理事件**：Subscriber 可以处理 Publisher 发出的值、完成事件和错误事件。
   - **取消订阅**：Subscriber 可以取消订阅，以停止接收事件并释放资源，通常使用 `store(in:)` 来管理生命周期。

3. **Operator（操作符）**：

   - **变换数据流**：Operator 用于操作和变换数据流，例如使用 `map` 运算符将值映射到新值。
   - **过滤数据**：Operator 允许你过滤数据流，例如使用 `filter` 运算符来选择特定的值。
   - **组合数据流**：Operator 允许你将多个数据流组合成一个，例如使用 `combineLatest` 运算符来组合多个数据流的最新值。

4. **Subscription（订阅）**：

   - **订阅管理**：Subscription 表示一个订阅关系，它跟踪着订阅的状态，包括活动状态和已取消状态。
   - **资源管理**：你可以使用 `store(in:)` 来管理订阅的生命周期，确保在不再需要时释放资源。
   - **背压处理**：Subscription 可以处理背压，它会适应 Publisher 和 Subscriber 的速度，以确保数据流平衡。

注意事项：

- 订阅是一种重要的概念，确保正确管理订阅的生命周期非常重要，以避免内存泄漏。
- 使用操作符时，要注意数据流的变换和组合，确保操作符的使用是正确的。
- Combine 的错误处理机制使用 `catch` 和 `retry` 操作符来处理错误，确保正确处理错误事件。
- Combine 的文档提供了丰富的示例和详细的说明，建议查阅文档以更好地理解这些概念和最佳实践。




### 4.3 发布者(Publishers）


发布者(Publishers），可以向对它感兴趣的订阅者发布数据。

在Combine框架中，发布者（Publishers）负责发布数据流或事件，并将这些数据流传递给对它们感兴趣的订阅者（Subscribers）。

Combine的核心思想是基于响应式编程，其中数据流被视为一个事件序列。发布者产生数据流，然后将其发送给订阅者。当发布者发布数据时，所有订阅该数据流的订阅者都会接收到这些数据，然后可以对数据进行处理、转换或执行其他操作。

下面是一个简单的示例，展示了如何在Combine中创建一个发布者并将数据发布给订阅者：

```swift
import Combine

// 创建一个发布者，它发布一个整数
let publisher = Just(42)

// 订阅者订阅发布者
let subscription = publisher.sink { value in
    print("Received value: \(value)")
}

// 在这里，发布者发布值42
```

在这个示例中，我们创建了一个名为`publisher`的发布者，它发布整数42。然后，我们使用`sink`操作符创建了一个订阅者，订阅者在接收到值42后会执行闭包并打印该值。

通过这种方式，发布者和订阅者之间建立了松散耦合的关系，发布者不需要知道有哪些订阅者，只需发布数据。这种模式在Combine框架中用于处理异步操作、事件流和数据处理，使得编写高效、可维护的异步代码变得更容易。


**需要考虑的问题**
什么时间点发送数据？
发送什么类型的数据？
发送多少次？
可以发送错误数据吗？
停止发送的条件？
发布者对象的生命周期？
还有没有其他的功能？
Combine框架中，提供了多少种发布者，如何使用？
其他，可以自定义？线程可以指定吗？
等等


### 4.4 运算符（Qperators）

运算符（Qperators），表现得像一个中转站，把发布者的数据进行处理后，然后再发布给另一个Operator或者订阅者。

在Combine框架中，运算符（Operators）充当中转站，用于对发布者的数据进行处理、转换或筛选，然后再将处理后的数据发布给下一个运算符或订阅者。运算符是Combine框架的一个关键概念，它们允许你以流水线的方式对数据流进行处理。

Combine提供了丰富的内置运算符，可以执行各种操作，包括数据映射、筛选、合并、组合等。你可以将多个运算符链接在一起，以创建复杂的数据处理流程。

以下是一个示例，演示了如何使用Combine运算符来处理数据流：

```swift
import Combine

// 创建一个发布者，发布整数
let publisher = Just(5)

// 使用运算符进行数据处理
let processedPublisher = publisher
    .map { $0 * 2 } // 将整数乘以2
    .filter { $0 > 5 } // 筛选出大于5的值

// 订阅者订阅处理后的发布者
let subscription = processedPublisher.sink { value in
    print("Received processed value: \(value)")
}
```

在这个示例中，我们首先创建一个发布者`publisher`，它发布整数5。然后，我们使用`map`运算符将整数乘以2，然后使用`filter`运算符筛选出大于5的值。最后，我们将订阅者订阅处理后的发布者`processedPublisher`，并在接收到处理后的值时打印它。

Combine的运算符非常强大，它们可以帮助你构建复杂的数据处理流程，同时保持代码的可读性和可维护性。这种流水线式的数据处理方式使得处理异步事件和数据流变得更加简单和高效。


**需要考虑的问题**
﻿如何接收发布者或者上一个Operator的数据，有什么限制？
﻿如何处理发布者或者上一个Operator的数据，有什么限制？
﻿如何把处理好的数据，发布给下一个Operator或订阅者？
﻿和前继或后继的数量关系，一对一，一对多或多对多？
﻿combine框架中，提供了多少种运算符，如何使用？


### 4.5 订阅者（ Subscribers）

订阅者（ Subscribers），最终处理发布者的数据（包括结束或异常数据）

订阅者（Subscribers）是Combine框架中的重要组件，它们最终处理来自发布者（Publishers）的数据流，包括正常的数据、结束事件和异常数据。订阅者订阅数据流，执行一些操作，然后根据数据流的完成状态或错误状态来执行适当的操作。

订阅者可以是任何订阅Combine数据流的组件，例如：

1. **sink**：`sink`是Combine中的一个常见订阅者，它用于执行闭包以处理数据流中的元素，以及处理完成或错误事件。`sink`可以用于打印数据、更新UI、执行其他操作等。

```swift
let publisher = Just(42)
let subscription = publisher.sink(
    receiveValue: { value in
        print("Received value: \(value)")
    },
    receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Received completion: Finished")
        case .failure(let error):
            print("Received completion: Error - \(error)")
        }
    }
)
```

2. **assign**：`assign`订阅者通常用于将数据流的值分配给对象属性，特别适用于SwiftUI中。

```swift
class ViewModel {
    @Published var data: Int = 0
}

let viewModel = ViewModel()
let publisher = Just(42)
let subscription = publisher.assign(to: \.data, on: viewModel)
```

3. **AnyCancellable**：`AnyCancellable`是Combine的订阅者包装，它允许你存储订阅关系并在不需要时取消订阅。这对于避免内存泄漏非常有用。

```swift
let publisher = Just(42)
let subscription = publisher.sink { value in
    print("Received value: \(value)")
}
let cancellable = subscription // 存储订阅关系
```

订阅者的主要任务是处理来自发布者的数据，包括数据值的接收和处理，以及对完成或错误事件的处理。这使得订阅者成为Combine中的一个关键组件，用于响应式编程和处理异步数据流。



**需要考虑的问题**
订阅者 如何接受数据（包括结束或异常数据）？
﻿订阅者订阅的数量，有无限制？
﻿订阅者作为订阅的终端，是否可以向发布者通知（好像不可以）？
﻿订阅者可以控制接受的数据次数吗
﻿combine框架中，订阅者有什么特点？



### 4.6 订阅（Subscriptions） 

订阅（Subscriptions），订阅是一个比较抽象的概念，代表着发布者，运算符，订问者的关系总和。combine框染，根据订阅(Subscription）描述的关系，进行调度。

订阅（Subscription）在Combine框架中是一个关键概念，它表示发布者（Publisher）、运算符（Operator）和订阅者（Subscriber）之间的关系总和。订阅描述了数据流的整个生命周期，包括数据流的创建、操作和订阅者的订阅行为。它还包括调度和管理数据流的操作。

以下是订阅的主要组成部分和概念：

1. **发布者（Publisher）**：发布者是数据流的源头，它生成和发布数据。发布者可以是任何遵循Combine框架中`Publisher`协议的类型，包括内置的发布者和自定义的发布者。

2. **运算符（Operator）**：运算符是用于处理、转换和操作数据流的操作。运算符可以链接在发布者上，以创建一个处理数据流的管道。每个运算符都返回一个新的发布者，这使得可以构建复杂的数据流处理链。

3. **订阅者（Subscriber）**：订阅者是最终处理数据流的组件，它订阅数据流并执行特定的操作，例如处理数据、更新UI或执行其他任务。订阅者通过调用`sink`、`assign`或其他方法来建立与发布者的关系。

4. **订阅（Subscription）**：订阅是数据流的一个具体实例，它描述了发布者、运算符和订阅者之间的关系。订阅包括数据流的配置，如何处理数据，以及如何处理完成或错误事件。订阅还可以用于取消数据流的订阅。

5. **调度器（Scheduler）**：调度器用于确定数据流在哪个线程上执行。Combine允许你使用不同的调度器来控制数据流的线程执行，以确保线程安全和合理的性能。

订阅是Combine框架中的一个抽象概念，它有助于描述数据流的关系和管理数据流的生命周期。通过建立订阅，你可以控制数据流的行为，例如何处理数据、何时取消订阅以及如何执行数据流上的操作。订阅还可以用于处理错误、完成事件和资源释放，以确保应用程序的稳定性和性能。



**需要考虑的问题**
﻿如何建立订阅？
﻿如何取消订阅？
被取消后的订阅是否可以继续开启，或者参与的发布对象等还可以重新使用？
订阅的参与对象（发布、运算符、订阅者）在Combine框架中，如何调度？
﻿﻿多个订阅之间，可以互相独立，也可以有关系？





## 5. Combine 基本演示和处理流程


Combine是一个强大的框架，用于处理异步数据流。下面是一个基本的Combine演示和处理流程，它包括创建发布者、使用运算符进行数据处理，以及订阅数据流的步骤：

```swift
import Combine

// 步骤1：创建一个发布者
let publisher = [1, 2, 3, 4, 5].publisher

// 步骤2：使用运算符进行数据处理
let processedPublisher = publisher
    .map { $0 * 2 } // 将每个元素乘以2
    .filter { $0.isMultiple(of: 3) } // 筛选出可以被3整除的元素

// 步骤3：订阅数据流
let subscription = processedPublisher.sink { value in
    print("Received processed value: \(value)")
}

// 输出：
// Received processed value: 6
```

上述示例的处理流程如下：

1. 步骤1：我们创建一个发布者 `publisher`，它发布了整数数组 `[1, 2, 3, 4, 5]` 的元素。

2. 步骤2：我们使用 `map` 运算符将发布者中的每个元素都乘以2，然后使用 `filter` 运算符筛选出可以被3整除的元素。这些运算符构成了运算符链，对数据流进行处理。

3. 步骤3：最后，我们订阅了 `processedPublisher`，这个处理后的发布者。当数据流流动时，`sink` 订阅者会接收并处理数据。在此示例中，只有值6符合筛选条件，因此只有6被打印出来。

Combine的强大之处在于，你可以创建复杂的运算符链，用于处理异步数据流，例如网络请求、用户输入、传感器数据等。这使得Combine成为构建高效、可维护和响应性的应用程序的强大工具。




关于Combine框架中的发布者（Publishers）和订阅者（Subscribers）的基本信息。

下面我将进一步解释这些概念：

**Publishers（发布者）**:

1. **Just**：`Just` 是一个发布者，用于发布单个确定的数值或值。它只发布一次，然后完成。这在需要发布一次性值的情况下非常有用。

```swift
import Combine

let publisher = Just(42)
```

2. **Future**：`Future` 是一个发布者，用于在未来某个时刻发布值。它需要一个闭包作为参数，该闭包在订阅时执行，并通知异步操作的结果。

```swift
import Combine

let publisher = Future<Int, Error> { promise in
    // 异步操作，例如网络请求
    let result = 42
    if result > 0 {
        promise(.success(result))
    } else {
        promise(.failure(MyError.someError))
    }
}
```

**Subscribers（订阅者）**:

1. **Sink**：`Sink` 订阅者是一种用于接收数据的通用订阅者。它接受两个闭包作为参数，`receiveCompletion` 用于处理订阅的完成事件，而 `receiveValue` 用于处理接收到的值。

```swift
import Combine

let publisher = Just(42)
let subscription = publisher.sink(
    receiveCompletion: { completion in
        switch completion {
            case .finished:
                print("Subscription completed.")
            case .failure(let error):
                print("Received error: \(error)")
        }
    },
    receiveValue: { value in
        print("Received value: \(value)")
    }
)
```

2. **Assign**：`Assign` 订阅者用于将数据分配给对象的属性，通常在SwiftUI中使用。它接受两个参数，一个对象和一个键路径（KeyPath），以确定要分配的属性。

```swift
import Combine

class ViewModel {
    @Published var data: Int = 0
}

let viewModel = ViewModel()
let publisher = Just(42)
let subscription = publisher.assign(to: \.data, on: viewModel)
```

Combine框架的发布者和订阅者模型提供了一种强大的方式来处理异步数据流，响应事件和构建响应式的应用程序。它允许你轻松地处理数据的流动，同时保持代码的可读性和可维护性。





### 5.1 Operators Map, Filter 进行演示

在Combine框架中，`map` 和 `filter` 是两个常用的操作符，用于处理发布者（Publishers）发布的数据流。它们允许你对数据进行映射和筛选，以满足特定的需求。

1. **Map**（映射）操作符：

   - **功能**：`map` 操作符用于将发布者发布的每个值进行映射、转换或变换，生成新的值，并将其发布给下游的订阅者。
   
   - **示例**：

     ```swift
     import Combine

     let publisher = [1, 2, 3, 4, 5].publisher

     let mappedPublisher = publisher.map { value in
         return value * 2 // 将每个值乘以2
     }

     let subscription = mappedPublisher.sink { value in
         print("Received value: \(value)")
     }
     ```

     在上面的示例中，`map` 操作符将发布者发布的每个整数值都乘以2，然后发布给订阅者，最终打印出处理后的值。

2. **Filter**（筛选）操作符：

   - **功能**：`filter` 操作符用于筛选发布者发布的值，只允许满足特定条件的值通过，而忽略不满足条件的值。

   - **示例**：

     ```swift
     import Combine

     let publisher = [1, 2, 3, 4, 5].publisher

     let filteredPublisher = publisher.filter { value in
         return value.isMultiple(of: 2) // 筛选出偶数值
     }

     let subscription = filteredPublisher.sink { value in
         print("Received value: \(value)")
     }
     ```

     在上面的示例中，`filter` 操作符筛选出了发布者发布的偶数值，然后发布给订阅者。

这些操作符是Combine框架中用于数据处理的基本工具，可以帮助你构建强大的数据流处理管道，以满足各种需求，包括数据转换、筛选、过滤等。操作符使得数据处理过程更加声明式和易于理解。


**注意**

在Combine的订阅者和发布者，数据类型必须一致，包括错误信息的类型也要一样。
为了能够更好的兼容既有的发布者和扩展。Combine定义了一些扩展来中转发送的数据，以方便对接订阅者的数据类型。
操作符是Combine 中非常重要的一部分，通过各式各样的操作符，
可以特原来各自不相关的逻辑变成一致的(unified）、声明式的 （dedlarative） 的数据流。
在Combine框架中要求发布者和订阅者的数据类型必须一致，包括错误信息的类型。这是因为Combine是一种强类型的框架，数据类型的一致性有助于确保类型安全和编译时检查。如果数据类型不一致，编译器将会报错。

为了兼容不同数据类型的发布者和订阅者，Combine提供了一些操作符（Operators）来进行数据类型的中转和转换。这些操作符允许你在数据流的处理过程中进行类型转换和适配，以确保数据流能够顺利传递。

以下是一些用于处理数据类型的常见Combine操作符：

1. **map**：`map` 操作符用于将发布者发布的值进行映射或转换为另一种数据类型。

```swift
let intPublisher = Just(42)
let stringPublisher = intPublisher.map { String($0) }
```

2. **flatMap**：`flatMap` 操作符用于处理嵌套的数据流，将内部数据流的值提取出来并发布。

```swift
let nestedPublisher = Just(Just(42))
let flatPublisher = nestedPublisher.flatMap { $0 }
```

3. **catch**：`catch` 操作符用于处理错误，可以将错误转换为另一种数据类型或重新发布数据。

```swift
let publisher = Fail<Int, MyError>(error: .someError)
let recoveredPublisher = publisher.catch { error in
    return Just(0) // 将错误转换为值
}
```

4. **replaceError**：`replaceError` 操作符用于替换错误，将错误替换为指定的值。

```swift
let publisher = Fail<Int, MyError>(error: .someError)
let replacedPublisher = publisher.replaceError(with: 0) // 将错误替换为0
```

Combine中的操作符允许你对数据流进行丰富的处理和转换，以适应不同的数据类型和需求。这有助于将不相关的逻辑整合为一致的、声明式的数据流，提高代码的可维护性和可读性。




在 Combine 中，基础的概念包括 Publisher（发布者）、Subscriber（订阅者）和 Operator（操作符）。这些概念是 Combine 的核心，用于创建、订阅和处理数据流。以下是它们的注意事项和区别：

1. **Publisher（发布者）**：

   - **基础数据流**：Publisher 是用于创建和发布数据流的类型。它可以发出值、完成事件或错误事件。
   - **注意事项**：
     - Publisher 应该是引用类型，因为多个订阅者可以订阅同一个 Publisher。
     - Publisher 不会执行任何操作，直到有订阅者订阅它。
     - Publisher 可以是单值的，也可以是多值的。
     - 使用 `eraseToAnyPublisher()` 可以抹去具体类型，使 Publisher 变为 AnyPublisher。

2. **Subscriber（订阅者）**：

   - **订阅数据流**：Subscriber 订阅 Publisher，以接收其发出的事件。Subscriber 通过 `sink` 方法来订阅 Publisher。
   - **处理事件**：Subscriber 可以处理 Publisher 发出的值、完成事件和错误事件。
   - **取消订阅**：Subscriber 可以取消订阅，以停止接收事件并释放资源。
   - **注意事项**：
     - Subscriber 被绑定到一个具体的 Publisher，它的类型需要匹配 Publisher 发出的值类型。
     - 使用 `store(in:)` 可以管理订阅的生命周期，避免内存泄漏。

3. **Operator（操作符）**：

   - **变换数据流**：Operator 用于操作和变换数据流，例如使用 `map` 运算符将值映射到新值。
   - **过滤数据**：Operator 允许你过滤数据流，例如使用 `filter` 运算符来选择特定的值。
   - **组合数据流**：Operator 允许你将多个数据流组合成一个，例如使用 `combineLatest` 运算符来组合多个数据流的最新值。
   - **注意事项**：
     - 操作符可以被链式使用，但需要谨慎使用，确保数据流的顺序和操作是正确的。
     - 操作符通常返回新的 Publisher，因此可以连续使用多个操作符。

**注意事项和区别**：

- 订阅者通常用于处理和消费数据流，而发布者用于创建和发出数据流。
- 一对多：一个 Publisher 可以有多个 Subscriber，但一个 Subscriber 只能订阅一个 Publisher。
- Publisher 是懒加载的，它只在有订阅者时才执行。
- 操作符是用于数据流的中间处理，它们不会执行，直到有订阅者订阅最终 Publisher。
- 订阅者的取消订阅是可选的，但为了避免内存泄漏，通常应该取消订阅。

了解这些基本概念的使用方法和区别是使用 Combine 框架的关键。正确管理订阅的生命周期和合理使用操作符是确保代码的可维护性和性能的重要方面。Combine 的文档和示例提供了更多详细信息，建议查阅以更深入地了解这些概念。




在 Combine 中，有许多常用的 Publisher（发布者）、Subscriber（订阅者）以及操作符，它们用于创建、处理和订阅数据流。以下是一些常见的 Publisher、Subscriber 和操作符：

**常用的 Publisher（发布者）**:

1. **Just**：创建一个只发出一次特定值的 Publisher。

```swift
let justPublisher = Just("Hello, Combine")
```

2. **PublishSubject**：一个可变的 Publisher，可以手动发出值，适用于多次值的场景。

```swift
let subject = PassthroughSubject<String, Never>()
```

3. **Future**：用于一次性发出一个值或错误的 Publisher。

```swift
let futurePublisher = Future<String, Error> { promise in
    // 异步操作后，使用 promise 发出值或错误
}
```

4. **NotificationCenter.Publisher**：用于订阅 NotificationCenter 通知的 Publisher。

```swift
let notificationPublisher = NotificationCenter.default.publisher(for: .someNotification)
```

5. **URLSession.DataTaskPublisher**：用于创建基于 URLSession 的数据任务的 Publisher。

```swift
let url = URL(string: "https://example.com/data.json")!
let dataTaskPublisher = URLSession.shared.dataTaskPublisher(for: url)
```

**常用的 Subscriber（订阅者）**:

1. **sink**：最常用的订阅者，用于处理 Publisher 发出的值、完成事件和错误事件。

```swift
publisher
    .sink(receiveValue: { value in
        print("Received value: \(value)")
    }, receiveCompletion: { completion in
        // 处理完成事件或错误事件
    })
    .store(in: &cancellables)
```

2. **assign**：用于将 Publisher 的值自动分配给绑定的属性。通常在 SwiftUI 中使用。

```swift
@Published var someValue: String = ""
publisher
    .assign(to: \.someValue, on: self)
    .store(in: &cancellables)
```

**常用的操作符**:

1. **map**：用于将 Publisher 发出的值进行转换。

```swift
publisher
    .map { value in
        return "Transformed \(value)"
    }
```

2. **filter**：用于过滤 Publisher 发出的值。

```swift
publisher
    .filter { value in
        return value > 10
    }
```

3. **combineLatest**：用于合并多个 Publisher 的最新值，例如，合并两个 Publisher 的最新值并将它们相加。

```swift
let combinedPublisher = Publisher1.combineLatest(Publisher2) { $0 + $1 }
```

4. **merge**：用于合并多个 Publisher 的值，无需在乎它们的顺序。

```swift
let mergedPublisher = Publisher1.merge(with: Publisher2)
```

5. **flatMap**：用于将 Publisher 发出的值映射到另一个 Publisher，并将它们合并。

```swift
publisher
    .flatMap { value in
        return AnotherPublisher(value)
    }
```

这只是 Combine 中一小部分常用 Publisher、Subscriber 和操作符的示例。Combine 提供了许多强大的工具，以便于处理和组合数据流。了解如何使用这些工具将使您能够更好地利用 Combine 来简化异步编程和数据流处理。建议查阅 Combine 框架的官方文档和示例以获取更多详细信息。





## 6. Combine 协议讲解

Combine 框架中有几个重要的协议，它们是 Combine 中核心概念的基础。以下是一些 Combine 中常见的协议以及它们的作用：

### 6.1 **Publisher 协议**：


孰悉Publisher协议
理解publiser执行上下文
理解Publisher订阅的过程


   - **Publisher** 协议定义了一个能够发出值、完成事件或错误事件的类型。它包括以下方法：
     - `subscribe<S>(_ subscriber: S) where S : Subscriber, Self.Failure == S.Failure, Self.Output == S.Input`：用于订阅 Publisher 的 Subscriber。
     - `receive<S>(subscriber: S) where S : Subscriber, Self.Failure == S.Failure, Self.Output == S.Input`：在订阅时，实际执行订阅操作的方法。

   `Publisher` 协议的实现通常包括数据流的创建和发出事件的逻辑。许多 Combine 框架中的发布者都实现了这个协议。


Publisher协议是Combine框架中的一个关键协议，它代表着可以发布数据流的类型。在Combine中，Publisher负责产生事件序列，将这些事件传递给订阅者，使得响应式编程成为可能。

下面是一些关于Publisher协议的关键概念：

- **Publisher协议定义**：Publisher协议定义了数据流的基本特征。它有两个关联类型，一个表示数据元素的类型（Output），另一个表示错误类型（Failure）。

```swift
protocol Publisher {
    associatedtype Output
    associatedtype Failure: Error

    func receive<S>(subscriber: S) where S : Subscriber, Self.Failure == S.Failure, Self.Output == S.Input
}
```

- **Publisher执行上下文**：Publisher可以在不同的执行上下文中工作，这意味着它可以在主线程、后台队列或其他线程中发布数据。这通常取决于Publisher的源头和数据的生成方式。例如，网络请求的Publisher可能在后台队列中执行，而UI事件的Publisher通常在主线程中执行。

- **Publisher订阅过程**：当一个订阅者希望接收数据流时，它可以订阅一个Publisher。订阅者通过调用Publisher的`subscribe(_:)`方法来发起订阅请求，传递一个Subscriber对象，Subscriber表示订阅者的需求。

```swift
let publisher: AnyPublisher<Int, MyError> = ...

let subscriber = MySubscriber()
publisher.subscribe(subscriber)
```

- **Publisher订阅的过程**：一旦订阅建立，Publisher会开始生成数据流，并将数据传递给Subscriber。Publisher可以产生以下事件：

  - 发布值（Value）：Publisher可以多次发布数据元素给Subscriber，每个数据元素的类型是Publisher中定义的`Output`类型。

  - 完成（Completion）：Publisher可以完成数据流，通知Subscriber数据流的结束。

  - 错误（Error）：Publisher可以遇到错误，通知Subscriber发生了错误。

Subscriber可以对这些事件进行响应，例如处理值、处理完成事件或处理错误。

理解Publisher协议和Publisher的订阅过程是理解Combine框架的关键。它使得你能够创建和管理数据流，以便在应用程序中以响应式的方式处理事件和数据。




### 6.2 **Subscriber 协议**：


熟悉Subscriber协办议
理解Subscriber和Subscription的关系
理解Subscriber的接受数据次数配置


   - **Subscriber** 协议定义了一个能够接收值、完成事件或错误事件的类型。它包括以下方法：
     - `receive(subscription: Subscription)`：接收发布者的订阅，通常在订阅时被调用。
     - `receive(_ input: Self.Input) -> Subscribers.Demand`：处理发布者发送的值，并返回订阅者的需求（Demand）。
     - `receive(completion: Subscribers.Completion<Self.Failure>)`：处理发布者发送的完成事件或错误事件。

   `Subscriber` 协议的实现通常包括数据流的接收和处理逻辑。许多 Combine 中的订阅者都实现了这个协议。


Subscriber协议是Combine框架中的另一个关键协议，它代表着订阅数据流的类型。Subscriber定义了如何处理从Publisher接收的数据、完成事件和错误事件。下面是一些关于Subscriber协议的关键概念：

- **Subscriber协议定义**：Subscriber协议定义了三个关联类型，分别表示输入数据类型（Input）、可能的错误类型（Failure）、以及用于订阅的上游订阅关系（Upstream）。

```swift
protocol Subscriber : Cancellable {
    associatedtype Input
    associatedtype Failure : Error

    func receive(subscription: Subscription)
    func receive(_ input: Self.Input) -> Subscribers.Demand
    func receive(completion: Subscribers.Completion<Self.Failure>)
}
```

- **Subscriber和Subscription的关系**：Subscriber和Subscription是紧密相关的，它们一起用于订阅数据流。当Subscriber发起订阅请求时，Publisher会创建一个Subscription对象，然后调用Subscriber的`receive(subscription:)`方法，将Subscription传递给Subscriber。Subscription表示订阅关系的生命周期，它允许Subscriber控制订阅的暂停、继续和取消。

```swift
protocol Subscription : Cancellable {
    func request(_ demand: Subscribers.Demand)
}
```

- **Subscriber的接受数据次数配置**：Subscriber的`receive(_:)`方法返回一个`Subscribers.Demand`值，该值表示Subscriber希望接收多少数据元素。这允许Subscriber控制从Publisher接收数据的速率。Demand可以是以下类型之一：

   - `.none`：表示Subscriber暂时不需要更多的数据。
   - `.unlimited`：表示Subscriber希望接收尽可能多的数据。
   - `.max(n)`：表示Subscriber希望接收不超过n个数据元素。

Subscriber可以根据其需求控制数据的接收速率。例如，它可以在处理一个数据元素后，请求更多的数据，或者将Demand设置为`.none`以暂时停止接收数据。

理解Subscriber和Subscription的关系以及Subscriber的接受数据次数配置是Combine框架中实现订阅关系和数据流控制的关键概念。它允许你以响应式的方式处理和管理数据流，同时控制数据的流动速率。




### 6.3 **Cancellable 协议**：

   - **Cancellable** 协议表示一个可以取消的对象，通常是用于取消订阅的对象。它定义了一个 `cancel()` 方法，用于执行取消操作，以停止接收发布者的事件。

   Combine 框架通常返回 `Cancellable` 对象，以便开发者可以在需要时取消订阅，避免资源泄漏。


`Cancellable` 是Combine框架中的一个协议，它代表可以取消订阅的对象。Cancellable协议的主要作用是提供一种方式来取消对数据流的订阅，以确保资源得到正确释放，并避免内存泄漏。

在Combine中，当你创建一个订阅时，通常会收到一个Cancellable对象，它代表了订阅的实际。通过调用Cancellable对象的`cancel`方法，你可以手动取消订阅，停止接收数据流，释放资源并停止订阅的生命周期。这对于确保资源的正确释放非常重要，特别是在需要在不再需要数据流时主动取消订阅的情况下。

以下是一个示例，演示了如何使用Cancellable对象来取消订阅：

```swift
import Combine

let publisher = Timer.publish(every: 1, on: .main, in: .default)
let cancellable = publisher.sink { value in
    print("Received value: \(value)")
}

// 取消订阅
cancellable.cancel()
```

在上面的示例中，我们使用`sink`方法订阅了一个定时器的发布者。然后，我们将返回的Cancellable对象存储在变量`cancellable`中。最后，通过调用`cancel`方法，我们手动取消订阅，停止接收数据流。

Cancellable协议的使用是确保在不再需要数据流时释放资源的关键机制，它有助于避免内存泄漏和资源泄漏问题。在Combine中，良好的取消订阅实践对于编写健壮的响应式应用程序至关重要。




### 6.4 **Subscription 协议**：

   - **Subscription** 协议用于表示订阅关系。它包括以下方法：
     - `request(_ demand: Subscribers.Demand)`：订阅者向发布者请求一定数量的值。
     - `cancel()`：取消订阅关系。

   `Subscription` 协议通常由发布者创建，以表示订阅关系，并用于控制数据流的传递。



在Combine框架中，`Subscription` 协议代表着一个订阅的生命周期，它负责管理订阅的行为，包括请求数据、取消订阅等操作。`Subscription` 是一个核心协议，被用于协调数据的流动和订阅的管理。

下面是关于 `Subscription` 协议的关键概念：

- **Subscription 协议定义**：Subscription 协议的定义如下：

```swift
protocol Subscription : Cancellable {
    func request(_ demand: Subscribers.Demand)
}
```

- **request(_:) 方法**：`Subscription` 协议要求实现一个 `request(_:)` 方法，用于向发布者请求数据。请求的数据量由 `Subscribers.Demand` 类型的参数表示。`Subscribers.Demand` 可以是以下之一：

   - `.none`：表示订阅者暂时不需要更多数据。
   - `.unlimited`：表示订阅者希望接收尽可能多的数据。
   - `.max(n)`：表示订阅者希望接收不超过 n 个数据元素。

请求数据的方式允许订阅者控制数据的流动速率，从而避免数据的过度传递或浪费。

- **Cancellable 协议**：`Subscription` 协议继承自 `Cancellable` 协议，因此 `Subscription` 也有 `cancel()` 方法，用于手动取消订阅。

通常，`Subscription` 是由 Combine 框架的 Publisher 创建并分配的，然后传递给订阅者。订阅者可以使用 `request(_:)` 方法来控制数据的接收速率，以及使用 `cancel()` 方法来手动取消订阅，释放资源并停止订阅的生命周期。

总之，`Subscription` 协议是 Combine 框架中用于管理订阅的生命周期和数据流动的关键协议，它允许订阅者与发布者之间进行有效的数据协调。




这些协议构成了 Combine 中数据流的基础，允许开发者创建、发布、订阅和处理数据流。理解这些协议有助于更好地使用 Combine 框架来简化异步编程和数据流处理。根据需要，您可以实现自定义的发布者、订阅者和订阅对象，以满足特定的需求。


### 6.5 **Subscribers.Demand次数配置** 

在Combine框架中，`Subscribers.Demand` 是一个用于配置订阅者（Subscriber）期望接收数据的类型。通过使用 `Subscribers.Demand`，订阅者可以控制从发布者（Publisher）接收数据的次数和速率。

`Subscribers.Demand` 具有以下三种可能的值：

1. **.none**：表示订阅者暂时不需要更多的数据。当订阅者的需求被设置为 `.none` 时，它告诉发布者暂时停止发送数据，等待进一步的需求。

2. **.unlimited**：表示订阅者希望接收尽可能多的数据。当订阅者的需求被设置为 `.unlimited` 时，它告诉发布者可以发送数据，而不受限制。

3. **.max(n)**：表示订阅者希望接收不超过 n 个数据元素。当订阅者的需求被设置为 `.max(n)` 时，它告诉发布者可以发送最多 n 个数据元素。

订阅者在订阅过程中可以使用 `Subscribers.Demand` 来通知发布者其数据需求。例如，订阅者可以通过向发布者发送 `Subscribers.Demand.unlimited` 来表明它希望尽可能多的数据。或者，订阅者可以发送 `Subscribers.Demand.max(n)` 来指定特定数量的数据。

这种需求配置允许订阅者有效地控制数据的流动速率，从而避免数据的过度传递或浪费。它还有助于处理背压（Backpressure）问题，即在订阅者处理速度不足的情况下，发布者如何适应减慢的数据消耗速率。

需要注意的是，订阅者通常会在处理数据后根据需要调整其需求，并根据情况向发布者发送新的 `Subscribers.Demand` 值。这使得数据流可以在双方之间得以协调，以确保数据的有效传递。



### 6.6 **执行上下文**

在 Combine 中，Publisher（发布者）的执行上下文（执行环境）和订阅过程都是重要的概念。执行上下文表示代码执行时的环境，而订阅过程涉及如何将订阅者与发布者关联在一起。以下是有关这两个概念的详细说明：

**1. Publisher 的执行上下文：**

在 Combine 中，Publisher 可以在不同的执行上下文中工作，这取决于其创建或操作符链中的操作符以及订阅的位置。执行上下文决定了代码的运行线程或队列。

- **主队列（Main Queue）**：许多 Combine 发布者（如 NotificationCenter.Publisher）在主队列上发出事件，以便在主线程上处理 UI 相关操作。

- **全局队列（Global Queue）**：一些 Combine 发布者，例如 URLSession.DataTaskPublisher，可能在后台线程上执行异步操作。

- **特定队列（Specific Queue）**：您可以使用 `receive(on:)` 操作符来明确指定执行上下文，以确保发布者事件在特定队列上执行。

**2. 订阅过程：**

订阅是将发布者与订阅者建立连接的过程，它涉及以下步骤：

- 创建发布者：首先，您创建一个 Combine 发布者，它可以是任何符合 Publisher 协议的类型。

- 创建订阅者：接下来，您创建一个 Combine 订阅者，它可以是一个 sink 操作或者符合 Subscriber 协议的类型。

- 执行订阅：使用 `sink` 操作符或 `assign` 操作符来执行订阅操作。这将建立发布者与订阅者之间的连接，并开始数据流的传递。

- 订阅者接收事件：一旦订阅完成，发布者可以开始向订阅者发送事件。这可能包括值、完成事件或错误事件，取决于发布者的行为。

- 处理事件：订阅者接收到发布者发送的事件后，执行相应的操作，例如处理值、处理完成事件或处理错误事件。

- 取消订阅：在订阅者不再需要接收事件时，您可以调用 `cancel()` 方法来取消订阅，以停止数据流传递。

在 Combine 中，订阅过程是按需启动的，这意味着发布者只有在有订阅者时才会执行，并且只有在有订阅者订阅后才会发出事件。这种懒加载的方式确保了效率和资源的有效使用。

**示例：**

以下是一个示例，演示了创建发布者、创建订阅者、执行订阅过程以及处理事件的步骤：

```swift
import Combine

let publisher = Just("Hello, Combine")
let cancellable = publisher.sink { value in
    print("Received value: \(value)")
}

// 输出：Received value: Hello, Combine

// 取消订阅
cancellable.cancel()
```

在这个示例中，我们创建了一个 Just 发布者，然后使用 `sink` 操作符订阅它。订阅完成后，发布者发出值，并订阅者处理这个值。最后，我们取消订阅以停止接收事件。



### 6.7 **前置 Swift知识**

熟悉Hashable定义
熟悉协议定义的方法 以及 关联类型约束条件
熟悉协议扩展定义方法
熟悉范型定义方法
理解Self和self的定义


在 Swift 中，`Hashable` 是一个协议，用于定义一个类型可以计算哈希值的能力。哈希值是一个固定长度的整数，通常用于在数据结构中快速查找和比较对象。`Hashable` 协议要求实现两个方法：

1. **hash(into:)** 方法：这个方法用于将类型的实例映射到哈希值。你需要在这个方法中计算一个哈希值并将其存储到传入的哈希容器中。

2. **== 运算符**：`Hashable` 协议还要求类型实现相等运算符 (`==`)，以便在哈希冲突时进行比较。

下面是一个使用 `Hashable` 协议的示例：

```swift
struct Person: Hashable {
    var name: String
    var age: Int
    
    func hash(into hasher: inout Hasher) {
        hasher.combine(name)
        hasher.combine(age)
    }
    
    static func == (lhs: Person, rhs: Person) -> Bool {
        return lhs.name == rhs.name && lhs.age == rhs.age
    }
}

let person1 = Person(name: "Alice", age: 30)
let person2 = Person(name: "Bob", age: 25)

print(person1.hashValue)
print(person2.hashValue)

if person1 == person2 {
    print("They are the same person.")
} else {
    print("They are different people.")
}
```

在上面的示例中，`Person` 结构体遵守了 `Hashable` 协议，实现了 `hash(into:)` 方法来计算哈希值，并实现了相等运算符来进行比较。你可以通过 `hashValue` 属性来获取对象的哈希值，以及使用相等运算符来比较对象是否相等。

哈希值是一种在集合类型（如 Set 和 Dictionary）中非常有用的功能，因为它可以帮助快速查找和存储对象。实现 `Hashable` 协议是在自定义类型中使用这些集合类型的关键一步。





你提到了几个与Swift编程相关的重要概念和特性，我将简要解释它们：

1. **Hashable定义**：

   `Hashable` 是Swift标准库中的一个协议，用于表示可以计算哈希值的类型。它要求类型提供一个`hashValue`属性或实现一个`hash(into:)`方法，以便可以为该类型的值计算唯一的哈希值。哈希值在集合（如字典和集合）中用于快速查找和存储元素。

2. **协议定义的方法**：

   在Swift中，协议可以定义方法的声明，但没有提供方法的具体实现。这些方法被称为协议方法。实现协议的类型必须提供这些方法的具体实现。例如：

   ```swift
   protocol SomeProtocol {
       func doSomething()
   }

   struct SomeStruct: SomeProtocol {
       func doSomething() {
           // 具体实现
       }
   }
   ```

3. **关联类型约束条件**：

   在协议定义中，可以使用关联类型来描述与协议关联的类型。关联类型用关键字`associatedtype`声明。你还可以在协议扩展中添加约束条件，以限制关联类型的类型。例如：

   ```swift
   protocol Container {
       associatedtype Item
       func addItem(_ item: Item)
   }

   extension Container where Item: Equatable {
       func contains(_ item: Item) -> Bool {
           // 实现
       }
   }
   ```

   在上面的示例中，`Item` 是关联类型，而`Container` 协议扩展添加了一个约束条件，要求关联类型`Item` 必须符合`Equatable` 协议。

4. **协议扩展定义方法**：

   协议扩展是在协议定义中提供默认方法实现的方式。它可以在协议中为方法提供默认行为，从而让遵循协议的类型获得这些方法的默认实现。例如：

   ```swift
   protocol Printable {
       func printMe()
   }

   extension Printable {
       func printMe() {
           print("Printing something")
       }
   }

   struct MyStruct: Printable {
       // 不需要提供printMe方法的具体实现
   }
   ```

5. **范型定义方法**：

   泛型是一种编程技术，允许编写适用于多种数据类型的可重用代码。在Swift中，你可以使用泛型类型、函数和方法来定义通用代码，以处理不同类型的数据。

   ```swift
   func swap<T>(_ a: inout T, _ b: inout T) {
       let temp = a
       a = b
       b = temp
   }
   ```

6. **Self和self的定义**：

   - `Self`（大写S）：`Self` 是一个特殊的关键字，用于表示当前类型的实例。它通常用在协议中，以指示实现协议的类型的实例。
   - `self`（小写s）：`self` 是一个引用当前实例的关键字。它用于访问当前实例的属性和方法。

7. **结合时序图进行协议定义**：

   时序图（Sequence Diagram）是一种UML图，用于可视化描述对象之间的交互。你可以使用时序图来描述协议定义和对象之间的交互，以展示协议方法的调用顺序和时序关系。

   时序图通常包括对象、生命线、消息和交互碎片等元素，以便清晰地表示对象之间的交互流程。你可以使用专业的建模工具或在线工具来创建时序图。

以上是一些与Swift编程相关的基本概念和特性，它们对于理解和编写Swift代码非常重要。结合时序图可以更好地可视化和理解协议定义和对象交互。






## 7. 结合协议讲解的代码示例

### 7.1 自定义一个简单的订阅者

要自定义一个简单的订阅者，你需要创建一个符合`Subscriber` 协议的类型，然后实现该协议的方法。下面是一个简单的示例，展示如何创建一个自定义的订阅者：

```swift
import Combine

class MySubscriber<Input, Failure: Error>: Subscriber {
    typealias Input = Input
    typealias Failure = Failure

    private var subscription: Subscription?

    init() { }

    func receive(subscription: Subscription) {
        self.subscription = subscription
        // 请求数据，例如 .unlimited 表示希望接收尽可能多的数据
        subscription.request(.unlimited)
    }

    func receive(_ input: Input) {
        // 处理接收到的数据
        print("Received data: \(input)")
    }

    func receive(completion: Subscribers.Completion<Failure>) {
        switch completion {
        case .finished:
            print("Subscription completed successfully.")
        case .failure(let error):
            print("Received error: \(error)")
        }
    }

    func cancel() {
        subscription?.cancel()
        subscription = nil
    }
}
```

在这个示例中，我们创建了一个名为 `MySubscriber` 的订阅者类，它可以处理任何类型的输入数据（`Input`）和错误类型（`Failure`）。该订阅者通过实现 `Subscriber` 协议的方法来处理订阅、接收数据和完成事件。

- `receive(subscription:)` 方法用于接收订阅关系，我们在这里请求了尽可能多的数据（`.unlimited`）。
- `receive(_:)` 方法用于处理接收到的数据。
- `receive(completion:)` 方法用于处理完成事件，包括成功完成和错误完成。
- `cancel()` 方法用于手动取消订阅，释放资源。

你可以创建一个 `MySubscriber` 实例并将其用于订阅发布者。当发布者发布数据时，`MySubscriber` 将处理数据、完成事件和错误事件，并在控制台打印相应的信息。

这只是一个简单的示例，你可以根据需要自定义更复杂的订阅者，以处理不同类型的数据和逻辑。




### 7.2 理解Future发布者的操作

`Future` 是Combine框架中的一个发布者类型，它用于表示将来会产生一个值或错误的异步操作。`Future` 可以用于封装一个将在未来某个时间点执行的操作，并在操作完成时向订阅者发布结果。

以下是一些关于`Future` 发布者的操作和示例：

1. **初始化 Future**：

   `Future` 的初始化需要一个闭包，该闭包包含将在未来执行的操作。闭包的参数是一个`Promise`对象，可以用于将结果传递给`Future` 的订阅者。

   ```swift
   let future = Future<String, Error> { promise in
       DispatchQueue.global().async {
           // 模拟异步操作
           if let result = performSomeAsyncTask() {
               promise(.success(result))
           } else {
               promise(.failure(MyError.someError))
           }
       }
   }
   ```

   在上面的示例中，`Future` 发布者封装了一个模拟的异步操作，根据操作的结果向订阅者发布成功值或错误。

2. **订阅 Future**：

   订阅`Future` 发布者与其他发布者相同，使用`sink`方法或其他订阅方法。

   ```swift
   let cancellable = future.sink(
       receiveCompletion: { completion in
           switch completion {
           case .finished:
               print("Future completed successfully.")
           case .failure(let error):
               print("Future completed with error: \(error)")
           }
       },
       receiveValue: { value in
           print("Received value: \(value)")
       }
   )
   ```

   订阅者可以在`Future` 执行完成后接收值或错误，并处理完成事件。

3. **取消 Future**：

   与其他发布者一样，你可以通过取消订阅来停止`Future` 发布者。取消订阅将阻止进一步的操作执行，并释放资源。

   ```swift
   cancellable.cancel()
   ```

`Future` 发布者常用于封装异步操作，例如网络请求或后台任务，以便以响应式的方式处理结果。它为将来的操作提供了一种方便的封装方式，并使操作的结果能够被合适地发布给订阅者。




### 7.3 理解Passthrough Subject发布者的操作 以及取消订阅


`PassthroughSubject` 是 Combine 中的一个发布者类型，它是一个可变的发布者，可以手动发出值并将这些值传递给订阅者。以下是关于 `PassthroughSubject` 发布者的常见操作和取消订阅的方法：

**1. 创建 `PassthroughSubject` 发布者**：

```swift
import Combine

let subject = PassthroughSubject<String, Error>()
```

上述代码创建了一个 `PassthroughSubject` 发布者，它发出字符串值，并可以传递错误。

**2. 发出值**：

使用 `send(_:)` 方法可以手动发出值给订阅者。

```swift
subject.send("Hello, Combine")
```

**3. 订阅 `PassthroughSubject` 发布者**：

使用 `sink` 方法或其他订阅操作符来订阅发布者。

```swift
subject.sink(receiveValue: { value in
    print("Received value: \(value)")
})
.store(in: &cancellables)
```

**4. 取消订阅**：

你可以通过调用 `cancel()` 方法来取消订阅。这通常在不再需要接收发布者事件时进行，以避免资源泄漏。

```swift
cancellable.cancel()
```

注意：`cancellable` 是 `sink` 方法返回的订阅对象，可以使用它来取消订阅。

**完整示例**：

```swift
import Combine

var cancellables: Set<AnyCancellable> = []

let subject = PassthroughSubject<String, Error>()

let cancellable = subject.sink(receiveValue: { value in
    print("Received value: \(value)")
})

subject.send("Hello, Combine")

// 取消订阅
cancellable.cancel()
```

在这个示例中，我们创建了一个 `PassthroughSubject` 发布者，并使用 `sink` 方法订阅它，然后手动发送一个值。最后，我们取消订阅，确保不再接收发布者的事件。

`PassthroughSubject` 是一种有用的发布者类型，适用于需要手动控制事件的情况，例如，当你需要将非 Combine 代码集成到 Combine 流中时。




`CurrentValueSubject` 是 Combine 框架中的一个特殊类型的发布者（Publisher），它具有一个初始值，并且可以随着时间的推移发出新值。它是 Combine 中的一个有状态的发布者，因为它始终具有一个当前值，该值可以随时被查询。下面是关于 `CurrentValueSubject` 的一些重要信息：

- `CurrentValueSubject` 实现了 `Subject` 协议，这使它可以充当发布者和订阅者之间的桥梁，允许您手动发送值，完成事件或错误事件。

- `CurrentValueSubject` 需要指定一个初始值，即在创建时就拥有一个初始值。

- 您可以使用 `send(_:)` 方法来手动发送值给订阅者。

- 订阅 `CurrentValueSubject` 时，订阅者将立即收到初始值（如果有的话）。

- 订阅者可以使用 `sink` 操作符或其他订阅方法订阅 `CurrentValueSubject`。

- `CurrentValueSubject` 可以随时更改其当前值，而所有已订阅的订阅者都将收到新的值。

- 它还具有错误事件和完成事件，可以通过 `send(completion:)` 和 `send(error:)` 方法发送。

以下是一个示例，演示了如何使用 `CurrentValueSubject`：

```swift
import Combine

// 创建一个初始值为0的CurrentValueSubject
let subject = CurrentValueSubject<Int, Never>(0)

// 订阅CurrentValueSubject
let cancellable = subject.sink { value in
    print("Received value: \(value)")
}

// 发送新值
subject.send(1)
subject.send(2)

// 输出:
// Received value: 0 (初始值)
// Received value: 1
// Received value: 2

// 更新当前值
subject.value = 3

// 输出:
// Received value: 3

// 取消订阅
cancellable.cancel()
```

在上面的示例中，我们创建了一个 `CurrentValueSubject`，它具有一个初始值 0。然后，我们订阅了它，发送了几个值，更新了当前值，并最后取消了订阅。订阅者会立即接收初始值，并在每次发送新值时得到通知。

`CurrentValueSubject` 在某些情况下非常有用，特别是当您需要在 Combine 流中保持一些状态时。它可以用作缓存或状态管理的工具，以及其他需要保持当前值的情况。




### 7.4 type Erasure 类型抹除

类型抹除（Type Erasure）是一种编程技巧，通常用于隐藏具体类型的细节，以使代码更灵活和通用。在Swift中，类型抹除通常涉及使用协议和泛型，以创建一个包装类型，该类型将具体类型包装在其内部，并通过协议暴露出特定的接口。

以下是一些关于类型抹除的概念和示例：

1. **类型抹除的需求**：

   类型抹除通常用于以下情况：

   - 隐藏具体类型的细节，以避免暴露实现细节。
   - 创建通用的容器或数据结构，以容纳不同类型的对象。
   - 在不知道具体类型的情况下，通过协议调用对象的方法。

2. **使用 Any 和 AnyObject**：

   在Swift中，`Any` 和 `AnyObject` 是两个用于类型抹除的特殊类型。`Any` 可以容纳任何类型的值，而 `AnyObject` 可以容纳任何类的实例。

   ```swift
   let anyValue: Any = 42
   let anyObject: AnyObject = UILabel()
   ```

3. **使用协议和泛型**：

   你可以使用协议和泛型来创建自定义的类型抹除容器。例如，以下是一个使用协议和泛型创建的类型抹除容器示例：

   ```swift
   protocol AnyPrinter {
       func print()
   }

   struct Printer<T>: AnyPrinter {
       private let value: T

       init(_ value: T) {
           self.value = value
       }

       func print() {
           Swift.print(value)
       }
   }
   ```

   在这个示例中，`AnyPrinter` 是一个协议，定义了一个 `print` 方法。`Printer` 结构使用泛型 `T` 来包装任何类型的值，并实现了 `AnyPrinter` 协议。这使得你可以将不同类型的值包装在 `Printer` 中，然后以 `AnyPrinter` 的形式调用 `print` 方法。

4. **类型擦除容器的使用**：

   ```swift
   let intPrinter: AnyPrinter = Printer(42)
   let stringPrinter: AnyPrinter = Printer("Hello, World")

   intPrinter.print() // 打印 42
   stringPrinter.print() // 打印 "Hello, World"
   ```

   在这里，`intPrinter` 和 `stringPrinter` 都是 `AnyPrinter` 类型的对象，它们可以容纳不同类型的值，并以通用的方式调用 `print` 方法。

类型抹除是一种强大的技术，可用于创建通用的数据结构和隐藏具体类型的细节。它在处理不同类型数据的情况下非常有用，同时保持代码的简洁性和灵活性。




### 7.5 自定义订阅者 Custorm Subscriber Sample

通过 o1_Custorm SUbscribersample学习：
如何自定义一个简单的订阅者
体会subscription.request的配置作用
如何计算接受发布数据的次数


在Combine中，自定义一个简单的订阅者可以让你更好地理解订阅者的工作原理以及如何配置`subscription.request`以控制数据接收的次数。让我们通过一个示例来学习如何自定义一个订阅者，理解`subscription.request`的作用，以及如何计算接收发布数据的次数。

假设我们有一个自定义的发布者`CustomPublisher`，它会发布一系列整数，我们想要自定义一个订阅者来接收这些整数，并计算接收的数据次数。首先，我们定义发布者和订阅者如下：

```swift
import Combine

// 自定义发布者
class CustomPublisher: Publisher {
    typealias Output = Int
    typealias Failure = Never

    func receive<S>(subscriber: S) where S : Subscriber, Failure == S.Failure, Output == S.Input {
        let subscription = CustomSubscription(subscriber: subscriber)
        subscriber.receive(subscription: subscription)
    }
}

// 自定义订阅者
class CustomSubscriber: Subscriber {
    typealias Input = Int
    typealias Failure = Never

    private var subscription: Subscription?

    init() { }

    func receive(subscription: Subscription) {
        self.subscription = subscription
        // 请求数据，例如 .unlimited 表示希望接收尽可能多的数据
        subscription.request(.unlimited)
    }

    func receive(_ input: Int) {
        // 处理接收到的数据
        print("Received data: \(input)")
    }

    func receive(completion: Subscribers.Completion<Never>) {
        print("Subscription completed successfully.")
    }

    func cancel() {
        subscription?.cancel()
        subscription = nil
    }

    func countReceivedData() {
        // 计算接收数据的次数
        // 使用变量或属性来记录接收次数
    }
}
```

在这个示例中，`CustomPublisher` 是自定义的发布者，它发布整数，而`CustomSubscriber` 是自定义的订阅者，用于接收这些整数并计算接收的数据次数。以下是一些关键点：

- `CustomPublisher` 实现了`receive(subscriber:)`方法，用于创建自定义的订阅关系。

- `CustomSubscriber` 实现了`receive(subscription:)`方法，它在接收订阅关系时请求尽可能多的数据（`.unlimited`）。

- `CustomSubscriber` 的`receive(_:)`方法用于处理接收到的数据，你可以在其中进行接收次数的计算。

- `CustomSubscriber` 还包括`countReceivedData()`方法，可以用来计算接收数据的次数。

接下来，你可以使用这些自定义的发布者和订阅者来创建订阅关系，并观察数据的接收次数。例如：

```swift
let customPublisher = CustomPublisher()
let customSubscriber = CustomSubscriber()

customPublisher.subscribe(customSubscriber)

// 等待一段时间...

customSubscriber.countReceivedData() // 获取接收数据的次数
```

这个示例演示了如何自定义一个订阅者，配置`subscription.request`来控制数据接收的次数，并在订阅者内部计算接收数据的次数。这有助于理解订阅者的工作原理和如何与发布者进行交互。




### 7.6 自定义发布者 Future Sample

学习使用 `Future` 发布者和了解 `Promise`，以及 `store` 接口和 `Result` 枚举的使用可以帮助你更好地理解 Combine 框架中处理异步操作的方式。

1. **学习 Future 发布者自定义**：

   `Future` 发布者用于表示将来会产生一个值或错误的异步操作。你可以自定义 `Future` 发布者，封装异步操作，并将结果发布给订阅者。以下是一个自定义 `Future` 发布者的示例：

   ```swift
   import Combine

   func performAsyncTask() -> Future<String, Error> {
       return Future { promise in
           DispatchQueue.global().async {
               if let result = doSomeAsyncWork() {
                   promise(.success(result))
               } else {
                   promise(.failure(MyError.someError))
               }
           }
       }
   }
   ```

   在这个示例中，`performAsyncTask` 函数返回一个 `Future` 发布者，它封装了一个模拟的异步操作。

2. **学习 Future 中 Promise 的定义和执行时间点**：

   `Promise` 是 `Future` 发布者内部用来处理异步操作结果的对象。它允许你在异步操作完成后执行 `promise(.success(...))` 或 `promise(.failure(...))` 来传递结果或错误给 `Future` 发布者的订阅者。`Promise` 的执行时间点取决于异步操作的完成时间。在上面的示例中，`promise` 在异步块中的某个时刻执行，根据操作结果传递值或错误给订阅者。

3. **store 接口的定义**：

   `store` 接口通常是指使用 Combine 框架中的 `Cancellable` 协议来存储订阅关系的对象。`Cancellable` 表示一个可取消的订阅，它有一个 `cancel` 方法，用于手动取消订阅。`store` 接口通常用于存储订阅，以便在需要时取消订阅，释放资源。

   例如，你可以这样使用 `store` 接口：

   ```swift
   var cancellables: Set<AnyCancellable> = []

   let publisher = Just(42)
   let cancellable = publisher.sink { value in
       print("Received value: \(value)")
   }
   cancellable.store(in: &cancellables)

   // 在适当的时候，可以通过以下方式取消订阅：
   // cancellables.forEach { $0.cancel() }
   ```

4. **Result 枚举型学习**：

   `Result` 枚举是 Swift 中的一种方式来表示函数执行的结果，可以是成功（包含值）或失败（包含错误）。它的定义如下：

   ```swift
   enum Result<Success, Failure: Error> {
       case success(Success)
       case failure(Failure)
   }
   ```

   `Result` 枚举常用于处理同步操作的结果，而 `Future` 发布者通常用于处理异步操作。当你使用 `Future` 时，通常会将异步操作的结果转化为 `Result` 枚举，然后使用 `promise` 来传递结果给订阅者。

学习这些概念和技术可以帮助你更好地理解和使用 Combine 框架中的异步操作和结果处理。




### 7.7 自定义发布者 Subiect Sample
让我们学习 Combine 中的 `Subject` 协议，以及两种常见的 `Subject` 类型：`PassthroughSubject` 和 `CurrentValueSubject`，以及如何使用 `subscription` 来取消订阅，以及如何使用 `store` 存储订阅。

1. **学习 Subject 协议定义**：

   `Subject` 是 Combine 框架中的协议，它既可以充当发布者又可以充当订阅者。这使得它成为一个非常有用的工具，可以用于创建自定义的数据流。`Subject` 协议定义如下：

   ```swift
   protocol Subject : AnyObject, Publisher {
       func send(_ value: Self.Output)
       func send(completion: Subscribers.Completion<Self.Failure>)
   }
   ```

   `Subject` 协议包括 `send(_:)` 方法，用于向订阅者发送值，以及 `send(completion:)` 方法，用于发送完成事件。

2. **学习 Passthrough Subject**：

   `PassthroughSubject` 是 `Subject` 协议的一种具体实现，它在订阅者和发布者之间传递数据，类似于一个管道。它可以发送任何类型的值，并不会保存最新值。

   ```swift
   import Combine

   let subject = PassthroughSubject<Int, Never>()

   // 发送数据
   subject.send(42)

   // 订阅
   let cancellable = subject.sink { value in
       print("Received value: \(value)")
   }
   ```

3. **订阅取消**：

   使用 `sink` 方法或其他订阅方法可以创建一个订阅关系，并返回一个 `Cancellable` 对象。通过调用 `cancel()` 方法，你可以手动取消订阅，停止接收数据流。

   ```swift
   let cancellable = subject.sink { value in
       print("Received value: \(value)")
   }

   // 取消订阅
   cancellable.cancel()
   ```

4. **使用 store**：

   使用 `store` 接口来存储订阅，以便在需要时取消订阅并释放资源。这通常是在管理多个订阅关系时非常有用的。

   ```swift
   var cancellables: Set<AnyCancellable> = []

   let subject = PassthroughSubject<Int, Never>()

   // 订阅
   let cancellable = subject.sink { value in
       print("Received value: \(value)")
   }

   cancellable.store(in: &cancellables)

   // 在适当的时候取消订阅：
   // cancellables.forEach { $0.cancel() }
   ```

5. **使用 CurrentValueSubject**：

   `CurrentValueSubject` 是 `Subject` 协议的另一种具体实现，它不仅可以发送值，还可以保存并发布最新值。它初始化时需要一个初始值。

   ```swift
   import Combine

   let subject = CurrentValueSubject<String, Never>("Initial Value")

   // 发送数据
   subject.send("New Value")

   // 获取当前值
   let currentValue = subject.value
   ```

   `CurrentValueSubject` 可以用于实现一些需要维护和发布当前状态的数据流。

这些概念和技术可以帮助你更好地理解和使用 Combine 框架中的 `Subject`，以及如何管理订阅和取消订阅。




你可以自定义一个 Combine Subject，使其符合 `Subject` 协议，以创建自己的数据流管理工具。以下是一个示例，展示如何创建一个自定义的 Subject，实现 `Subject` 协议的方法，包括 `send(_:)` 和 `send(completion:)`。

```swift
import Combine

// 自定义 Subject
class MyCustomSubject<Output, Failure: Error>: Subject {
    typealias Output = Output
    typealias Failure = Failure

    private var subscribers: [AnySubscriber<Output, Failure>] = []

    func send(_ value: Output) {
        for subscriber in subscribers {
            _ = subscriber.receive(value)
        }
    }

    func send(completion: Subscribers.Completion<Failure>) {
        for subscriber in subscribers {
            subscriber.receive(completion: completion)
        }
    }

    func receive<S>(subscriber: S) where S: Subscriber, Failure == S.Failure, Output == S.Input {
        let anySubscriber = AnySubscriber(subscriber)
        subscribers.append(anySubscriber)
        subscriber.receive(subscription: MyCustomSubscription(subscriber: anySubscriber, subject: self))
    }

    func removeSubscriber(_ subscriber: AnySubscriber<Output, Failure>) {
        if let index = subscribers.firstIndex(where: { $0 === subscriber }) {
            subscribers.remove(at: index)
        }
    }
}

// 自定义 Subscription
class MyCustomSubscription<Output, Failure: Error>: Subscription {
    private var subscriber: AnySubscriber<Output, Failure>?
    private var subject: MyCustomSubject<Output, Failure>?

    init(subscriber: AnySubscriber<Output, Failure>, subject: MyCustomSubject<Output, Failure>) {
        self.subscriber = subscriber
        self.subject = subject
    }

    func request(_ demand: Subscribers.Demand) {
        // Handle demand if needed
    }

    func cancel() {
        subject?.removeSubscriber(subscriber!)
        subject = nil
        subscriber = nil
    }
}
```

在上面的示例中，我们创建了一个名为 `MyCustomSubject` 的自定义 Subject，该 Subject 可以发送值和完成事件给订阅者。我们还实现了一个名为 `MyCustomSubscription` 的自定义 Subscription，用于管理订阅关系。

你可以使用这个自定义 Subject 来创建和管理自己的数据流。注意，这个示例是一个简化的示例，实际中可能需要更多的逻辑和错误处理。自定义 Subject 可以用于处理特定的数据流需求或为 Combine 框架增加自定义行为。



7.8 typeErasure类型擦除

`AnyPublisher` 是 Combine 框架中的类型，它用于类型擦除，将不同类型的发布者封装到一个不透明的通用类型中。这与 SwiftUI 中的 `AnyView` 类似，它可以隐藏不同类型的视图。

以下是如何使用 `AnyPublisher` 进行类型擦除的示例：

```swift
import Combine

// 假设有一个自定义的发布者
let customPublisher: AnyPublisher<String, Error> = CustomPublisher()

// 使用 eraseToAnyPublisher() 方法将其转换为 AnyPublisher
let erasedPublisher: AnyPublisher<String, Error> = customPublisher.eraseToAnyPublisher()
```

在这个示例中，`CustomPublisher` 是一个自定义的发布者，它发布字符串类型的数据。通过使用 `eraseToAnyPublisher()` 方法，我们将其类型擦除为 `AnyPublisher<String, Error>`，从而隐藏了具体的发布者类型。

在 SwiftUI 中，`AnyView` 类似地用于类型擦除，使你可以隐藏不同类型的视图。这对于创建通用的视图层次结构以及根据需要更改视图类型非常有用。以下是一个示例：

```swift
import SwiftUI

struct ContentView: View {
    var body: some View {
        if condition {
            return AnyView(Text("Hello, World"))
        } else {
            return AnyView(Image(systemName: "star.fill"))
        }
    }
}
```

在这个示例中，`AnyView` 允许你在视图层次结构中包装不同类型的视图，就像 `AnyPublisher` 允许你在 Combine 数据流中包装不同类型的发布者。这增加了灵活性，并允许你在需要时切换不同类型的视图或发布者。






## 8. 转换操作符Transforming Operators

 各种Transforming Operators
collect, map, flatMap, replace Nil, replaceEmpty, scan
理解map的逻辑转换。
理解flatMap的工作机制。
理解scan 和reduce的区别。

### 8.1 常用操作符 collect, map, flatMap, replace Nil, replaceEmpty, scan

Combine 中的 Transforming Operators（变换操作符）用于对数据流执行不同的数据转换和处理操作，以生成新的数据流。这些操作符可以帮助你处理、过滤、映射、拆分、合并、以及转换数据，以满足你的需求。以下是一些常见的 Transforming Operators 以及它们的简要介绍：

这里简要介绍了常用的 Combine 操作符，包括 `collect`、`map`、`flatMap`、`replaceNil`、`replaceEmpty` 和 `scan`。

1. **`collect` 操作符**：

   `collect` 操作符用于将数据流中的多个元素收集到一个数组中，并将整个数组作为一个元素发布。这对于批量处理数据非常有用。以下是一个示例：

   ```swift
   let publisher = (1...5).publisher
   let collectedPublisher = publisher.collect()
   _ = collectedPublisher.sink { values in
       print("Collected values: \(values)")
   }
   // 输出: Collected values: [1, 2, 3, 4, 5]
   ```

2. **`map` 操作符**：

   `map` 操作符用于将数据流中的每个元素应用一个闭包函数，从而转换成新的元素。以下是一个示例：

   ```swift
   let publisher = (1...5).publisher
   let mappedPublisher = publisher.map { $0 * 2 }
   _ = mappedPublisher.sink { value in
       print("Mapped value: \(value)")
   }
   // 输出: Mapped value: 2, 4, 6, 8, 10
   ```

3. **`flatMap` 操作符**：

   `flatMap` 操作符用于将数据流中的元素转换为新的数据流，然后将这些数据流合并成一个输出数据流。以下是一个示例：

   ```swift
   let publisher = [1, 2, 3].publisher
   let flatMappedPublisher = publisher.flatMap { value in
       return [value, value * 2].publisher
   }
   _ = flatMappedPublisher.sink { value in
       print("FlatMapped value: \(value)")
   }
   // 输出: FlatMapped value: 1, 2, 2, 4, 3, 6
   ```

4. **`replaceNil` 操作符**：

   `replaceNil` 操作符用于将数据流中的 `nil` 值替换为指定的非空值。以下是一个示例：

   ```swift
   let values: [Int?] = [1, nil, 3, nil, 5]
   let publisher = values.publisher
   let replacedPublisher = publisher.replaceNil(with: 0)
   _ = replacedPublisher.sink { value in
       print("Replaced value: \(value)")
   }
   // 输出: Replaced value: 1, Replaced value: 0, Replaced value: 3, Replaced value: 0, Replaced value: 5
   ```

5. **`replaceEmpty` 操作符**：

   `replaceEmpty` 操作符用于在数据流为空时，替换为指定的默认元素。以下是一个示例：

   ```swift
   let emptyPublisher = Empty<Int, Never>()
   let replacedPublisher = emptyPublisher.replaceEmpty(with: 42)
   _ = replacedPublisher.sink { value in
       print("Replaced value: \(value)")
   }
   // 输出: Replaced value: 42
   ```

6. **`scan` 操作符**：

   `scan` 操作符用于将数据流中的元素逐步累积，生成一个累积的结果。以下是一个示例：

   ```swift
   let publisher = (1...5).publisher
   let scannedPublisher = publisher.scan(0, +)
   _ = scannedPublisher.sink { value in
       print("Scanned value: \(value)")
   }
   // 输出: Scanned value: 1, Scanned value: 3, Scanned value: 6, Scanned value: 10, Scanned value: 15
   ```


7. **`compactMap` 操作符**：用于将数据流中的元素映射为可选类型，然后过滤掉为 nil 的结果。

   ```swift
   let publisher = ["1", "2", "three", "4"].publisher
   let compactMappedPublisher = publisher.compactMap { Int($0) }
   ```

8. **`filter` 操作符**：用于根据提供的条件过滤数据流中的元素。

   ```swift
   let publisher = [1, 2, 3, 4, 5].publisher
   let filteredPublisher = publisher.filter { $0 % 2 == 0 } // 过滤偶数
   ```


9. **`merge` 操作符**：用于合并多个数据流为一个输出数据流。

   ```swift
   let publisher1 = [1, 2, 3].publisher
   let publisher2 = [4, 5, 6].publisher
   let mergedPublisher = Publishers.Merge(publisher1, publisher2)
   ```

10. **`combineLatest` 操作符**：用于将多个数据流的最新值组合成一个元组。

   ```swift
   let publisher1 = [1, 2, 3].publisher
   let publisher2 = ["A", "B", "C"].publisher
   let combinedPublisher = publisher1.combineLatest(publisher2)
   ```

11. **`zip` 操作符**：用于将多个数据流的对应元素组合成一个元组。

   ```swift
   let publisher1 = [1, 2, 3].publisher
   let publisher2 = ["A", "B", "C"].publisher
   let zippedPublisher = Publishers.Zip(publisher1, publisher2)
   ```


这些操作符可以帮助你处理和转换 Combine 数据流，根据需要执行不同的操作，例如收集数据、映射元素、合并数据流、替换值等。你可以根据具体情况选择适当的操作符来满足你的需求。


### 8.2 理解map的逻辑转换

`map` 是 Combine 中的一个常用操作符，它用于对数据流中的每个元素执行逻辑转换，生成新的元素。`map` 操作符的逻辑转换如下：

1. `map` 操作符接受一个闭包函数作为参数，这个闭包函数的输入类型应该与数据流中的元素类型相匹配，而输出类型可以是任何你希望生成的类型。

2. 当数据流中的元素到达时，`map` 操作符会将这个元素传递给闭包函数，然后将闭包函数的输出作为新的元素发布到输出数据流中。

3. 通过 `map` 操作符，你可以将数据流中的元素进行各种逻辑转换，例如从整数到字符串的转换、从 JSON 数据到自定义模型对象的映射，或者应用任何自定义逻辑。

以下是一个示例来说明 `map` 操作符的逻辑转换：

```swift
import Combine

let publisher = (1...5).publisher

let mappedPublisher = publisher.map { number in
    return "Number: \(number)"
}

_ = mappedPublisher.sink { value in
    print("Mapped value: \(value)")
}
```

在这个示例中，原始数据流包含整数，而 `map` 操作符将每个整数转换为一个字符串，附加了 "Number: " 前缀。所以输出将包含了这些转换后的字符串。

`map` 操作符在许多情况下非常有用，它允许你对数据流中的元素进行灵活的逻辑转换，以生成适合你需求的新元素。这对于数据处理、数据格式转换和模型映射非常有帮助。




### 8.3 理解flatMap的工作机制

`flatMap` 是 Combine 中的操作符，用于将数据流中的每个元素转换为新的数据流，然后将这些数据流合并成一个输出数据流。它的工作机制如下：

1. `flatMap` 操作符接受一个闭包函数作为参数，这个闭包函数的输入类型应该与数据流中的元素类型相匹配，而输出类型应该是另一个数据流（也就是 `Publisher`）。

2. 当数据流中的元素到达时，`flatMap` 操作符会调用闭包函数，并传递该元素作为参数。闭包函数的任务是返回一个新的数据流（`Publisher`），这个数据流可以是任何类型，包括异步操作、网络请求、另一个数据流等。

3. `flatMap` 操作符将这些返回的新数据流合并成一个输出数据流，即它会订阅这些新数据流，并将它们的元素合并到输出数据流中。

4. 输出数据流中的元素的顺序可能会受到新数据流完成的时间点的影响，因为 `flatMap` 操作符会等待新数据流的完成事件。

以下是一个示例来说明 `flatMap` 操作符的工作机制：

```swift
import Combine

let inputPublisher = PassthroughSubject<Int, Never>()

let flatMappedPublisher = inputPublisher.flatMap { value in
    return Just(value * 2).delay(for: .seconds(1), scheduler: RunLoop.main)
}

_ = flatMappedPublisher.sink { value in
    print("Received value: \(value)")
}

inputPublisher.send(1)
inputPublisher.send(2)
```

在这个示例中，`inputPublisher` 发布整数元素，而 `flatMap` 操作符将每个整数元素转换为一个 `Just` 发布者，这个发布者会将原始值乘以2，并延迟1秒后发布。`flatMap` 操作符合并了这些新数据流，所以在输出中你会看到这些值按照延迟的时间点逐个出现。

`flatMap` 在处理嵌套的数据流、异步操作、以及需要合并多个数据流的情况下非常有用。它允许你处理和合并多个数据流，以便进行更复杂的数据处理和操作。




### 8.4 理解scan 和reduce的区别

`scan` 和 `reduce` 都是用于累积值的 Combine 操作符，但它们之间有一些关键区别：

1. **`scan` 操作符**：
   - `scan` 用于逐步累积数据流中的元素，将每个元素应用于指定的闭包函数，并将结果作为下一个元素的一部分发布。
   - 它生成一个新的数据流，其中包含所有中间累积的值，包括初始值和最终结果。
   - `scan` 不会生成一个单一的最终结果，而是为每个元素生成一个中间结果。

   ```swift
   let publisher = (1...5).publisher
   let scannedPublisher = publisher.scan(0, +)
   // 输出: Scanned value: 1, Scanned value: 3, Scanned value: 6, Scanned value: 10, Scanned value: 15
   ```

2. **`reduce` 操作符**：
   - `reduce` 用于将数据流中的元素逐步合并为单一的最终结果。
   - 它需要一个初始值和一个闭包函数，将每个元素与当前累积值进行合并，并生成最终结果。
   - `reduce` 返回一个单一的值，而不是一个数据流。

   ```swift
   let publisher = (1...5).publisher
   let reducedPublisher = publisher.reduce(0, +)
   // 输出: Reduced value: 15
   ```

总结区别：
- `scan` 用于生成包含所有中间累积值的数据流，适用于需要查看数据流中每个步骤的情况。
- `reduce` 用于将数据流中的元素合并为单一的最终结果，适用于需要一个最终结果的情况。

你可以根据具体需求选择使用 `scan` 或 `reduce` 操作符。如果你需要查看数据流中每个步骤的中间结果，使用 `scan`。如果你只关心最终结果，使用 `reduce`。




 
## 9. 过滤操作符 Filtering Operators


> 学习各种Filtering Operators
> 
> filter,removeDuplicate,compactMap.ignore Qutput, drop,prefix
> 
> 理解compactMap的工作机制。
> 
> 理解drop 和prefix的untilQutputFrom 参数。


### 9.1 常用的操作符Filtering Operators

Combine 提供了一系列用于数据筛选和过滤的 Filtering Operators（过滤操作符）。以下是常见的过滤操作符，以及它们的简要介绍：

1. **`filter` 操作符**：

   `filter` 操作符用于根据提供的条件过滤数据流中的元素，只保留满足条件的元素。

   ```swift
   let publisher = (1...10).publisher
   let filteredPublisher = publisher.filter { $0 % 2 == 0 } // 保留偶数
   ```

2. **`removeDuplicates` 操作符**：

   `removeDuplicates` 操作符用于去除数据流中重复的连续元素，只保留第一次出现的元素。

   ```swift
   let publisher = [1, 1, 2, 2, 3, 3, 4].publisher
   let distinctPublisher = publisher.removeDuplicates() // 去除重复元素
   ```

3. **`compactMap` 操作符**：

   `compactMap` 操作符用于将数据流中的元素映射为可选类型，然后过滤掉为 `nil` 的结果。

   ```swift
   let publisher = ["1", "2", "three", "4"].publisher
   let compactMappedPublisher = publisher.compactMap { Int($0) }
   ```

4. **`ignoreOutput` 操作符**：

   `ignoreOutput` 操作符用于忽略数据流中的所有元素，只关心完成事件或错误事件。

   ```swift
   let publisher = (1...5).publisher
   let ignoredPublisher = publisher.ignoreOutput()
   ```

5. **`drop` 操作符**：

   `drop` 操作符用于跳过数据流中的前几个元素，只保留后续的元素。

   ```swift
   let publisher = (1...10).publisher
   let droppedPublisher = publisher.dropFirst(3) // 跳过前3个元素
   ```

6. **`prefix` 操作符**：

   `prefix` 操作符用于只保留数据流中的前几个元素。

   ```swift
   let publisher = (1...10).publisher
   let prefixedPublisher = publisher.prefix(5) // 保留前5个元素
   ```

这些过滤操作符允许你根据特定条件筛选或处理数据流中的元素，以便满足你的需求。你可以根据具体情况选择适当的操作符，以进行数据流的筛选和过滤。




### 9.2 理解compactMap的工作机制

`compactMap` 是 Combine 中的操作符，它的主要功能是将数据流中的元素映射为可选类型，然后过滤掉结果为 `nil` 的元素。以下是 `compactMap` 操作符的工作机制：

1. `compactMap` 操作符接受一个闭包函数作为参数，这个闭包函数的输入类型应该与数据流中的元素类型相匹配，而输出类型应该是可选类型（`Optional`）。

2. 当数据流中的元素到达时，`compactMap` 操作符会调用闭包函数，并将元素传递给它。

3. 闭包函数的任务是将元素映射为一个可选值（可能是一个非空值或 `nil`）。

4. 如果闭包函数返回的是一个非空可选值，那么该值将包含在输出数据流中。

5. 如果闭包函数返回的是 `nil`，那么该元素将被过滤掉，不会出现在输出数据流中。

以下是一个示例来说明 `compactMap` 操作符的工作机制：

```swift
import Combine

let publisher = ["1", "2", "three", "4"].publisher

let compactMappedPublisher = publisher.compactMap { value in
    return Int(value)
}

_ = compactMappedPublisher.sink { value in
    print("Mapped value: \(value)")
}
```

在这个示例中，原始数据流包含字符串，而 `compactMap` 操作符将每个字符串尝试转换为整数。只有 "1"、"2" 和 "4" 能够成功转换，而 "three" 无法转换为整数，所以它被过滤掉。结果中只包含了整数值。

`compactMap` 操作符通常用于处理可能包含无效或不必要元素的数据流，它将这些元素过滤掉，并将有效的元素保留下来，以便进一步处理。这在数据流处理中非常有用，尤其是在数据清理和验证方面。




### 9.3 理解drop 和prefix的untilQutputFrom 参数

`drop` 和 `prefix` 操作符在 Combine 中可以使用 `untilOutputFrom` 参数来控制它们的行为。这个参数允许你指定一个信号（另一个数据流），并且只有在该信号产生输出时，`drop` 和 `prefix` 操作符才会开始生效。这是一种在处理多个数据流之间协调行为的方式。

以下是 `drop` 和 `prefix` 操作符中 `untilOutputFrom` 参数的用法示例：

```swift
import Combine

let mainPublisher = PassthroughSubject<Int, Never>()
let triggerPublisher = PassthroughSubject<Void, Never>()

let droppedPublisher = mainPublisher
    .drop(untilOutputFrom: triggerPublisher)
    
let prefixedPublisher = mainPublisher
    .prefix(untilOutputFrom: triggerPublisher)

_ = droppedPublisher.sink { value in
    print("Dropped: \(value)")
}

_ = prefixedPublisher.sink { value in
    print("Prefixed: \(value)")
}

mainPublisher.send(1)
mainPublisher.send(2)
triggerPublisher.send()
mainPublisher.send(3)
```

在上面的示例中，`mainPublisher` 是主要的数据流，而 `triggerPublisher` 是触发器数据流。`drop` 和 `prefix` 操作符都使用 `untilOutputFrom: triggerPublisher` 参数，这意味着它们将等待 `triggerPublisher` 发出信号后才会开始生效。

当我们发送了两个值到 `mainPublisher` 后，没有任何输出，因为 `triggerPublisher` 还没有发出信号。然后，当我们发送信号到 `triggerPublisher` 时，`drop` 操作符开始生效，丢弃 `mainPublisher` 发出的值。与此同时，`prefix` 操作符也开始生效，只保留 `mainPublisher` 发出的值。所以，输出结果如下：

```
Prefixed: 1
Prefixed: 2
Dropped: 3
```

`drop` 和 `prefix` 操作符的 `untilOutputFrom` 参数可用于控制何时开始处理数据，这对于需要协调多个数据流的场景非常有用。





## 10. Combine Operators


学习各种Combine Operators
prepend , append,switch ToLatest merge, combineLatest,zip.
理解switchToLatest的工作机制
理解combinelatest 和zip的区别


### 10.1 常用的操作符Combine Operators

以下是常用的 Combine 操作符，包括 `prepend`、`append`、`switchToLatest`、`merge`、`combineLatest` 和 `zip` 的简要介绍：

1. **`prepend` 操作符**：

   `prepend` 操作符用于在数据流的开头添加元素或其他数据流。它可以用于插入元素，将数据流分为多个部分，或者添加头部信息。

   ```swift
   let numbers = (1...3).publisher
   let prefixedPublisher = [0].publisher.prepend(numbers)
   ```

2. **`append` 操作符**：

   `append` 操作符用于在数据流的末尾添加元素或其他数据流。它可以用于追加元素，将数据流分为多个部分，或者添加尾部信息。

   ```swift
   let numbers = (1...3).publisher
   let appendedPublisher = numbers.append(4)
   ```

3. **`switchToLatest` 操作符**：

   `switchToLatest` 操作符用于在数据流中处理其他数据流，将最新的数据流的元素发布到输出数据流中。这对于处理嵌套的数据流非常有用。

   ```swift
   let mainPublisher = PassthroughSubject<Publisher<Int, Never>, Never>()
   let switchedPublisher = mainPublisher.switchToLatest()
   ```

4. **`merge` 操作符**：

   `merge` 操作符用于合并多个数据流成为一个输出数据流，不考虑元素的顺序。它将所有数据流的元素按照它们的到达顺序发布到输出数据流中。

   ```swift
   let publisher1 = [1, 2, 3].publisher
   let publisher2 = [4, 5, 6].publisher
   let mergedPublisher = Publishers.Merge(publisher1, publisher2)
   ```

5. **`combineLatest` 操作符**：

   `combineLatest` 操作符用于将多个数据流中的最新元素进行组合，并在任一数据流发出新元素时更新输出数据流。输出的元素是由最新的各个数据流元素组成的元组。

   ```swift
   let publisher1 = PassthroughSubject<Int, Never>()
   let publisher2 = PassthroughSubject<String, Never>()
   let combinedPublisher = publisher1.combineLatest(publisher2)
   ```

6. **`zip` 操作符**：

   `zip` 操作符用于将多个数据流的元素一一配对，只有当每个数据流都有新元素时才会发布新的元素。它会生成一系列元素对的序列。

   ```swift
   let publisher1 = [1, 2, 3].publisher
   let publisher2 = ["A", "B", "C"].publisher
   let zippedPublisher = Publishers.Zip(publisher1, publisher2)
   ```

这些操作符可用于合并、扩展、组合和分割数据流，使数据流处理更加灵活和强大。你可以根据需要选择适当的操作符来满足你的需求。




### 10.2 理解switchToLatest的工作机制

`switchToLatest` 操作符是 Combine 中的一种操作符，用于处理嵌套的数据流。它的工作机制如下：

1. `switchToLatest` 操作符接受一个初始数据流，该数据流的元素本身是其他数据流（内部数据流）。

2. 当初始数据流的元素到达时，`switchToLatest` 操作符会自动订阅并处理该元素代表的内部数据流。

3. 内部数据流中的元素将被发布到输出数据流中。这意味着 `switchToLatest` 操作符将"切换"到最新的内部数据流，并处理它。

4. 如果初始数据流发出另一个元素（代表不同的内部数据流），`switchToLatest` 操作符将取消订阅之前的内部数据流，并开始处理新的内部数据流。

5. 内部数据流可以是任何 Combine 发布者，包括 PassthroughSubject、Just、Timer 等。

以下是一个示例来说明 `switchToLatest` 操作符的工作机制：

```swift
import Combine

let mainPublisher = PassthroughSubject<Publisher<Int, Never>, Never>()

let switchedPublisher = mainPublisher.switchToLatest()

let firstPublisher = PassthroughSubject<Int, Never>()
let secondPublisher = PassthroughSubject<Int, Never>()

_ = switchedPublisher.sink { value in
    print("Received: \(value)")
}

mainPublisher.send(firstPublisher)
firstPublisher.send(1)
firstPublisher.send(2)

mainPublisher.send(secondPublisher)
secondPublisher.send(3)

mainPublisher.send(firstPublisher)
firstPublisher.send(4)
```

在这个示例中，`mainPublisher` 发出两个内部数据流，分别是 `firstPublisher` 和 `secondPublisher`。`switchToLatest` 操作符会在每次切换到最新的内部数据流时，接收和处理来自该内部数据流的元素。

输出结果如下：

```
Received: 1
Received: 2
Received: 3
Received: 4
```

注意：`switchToLatest` 操作符通常用于处理动态生成的数据流，例如网络请求或用户事件。当需要切换到最新的数据流时，它非常有用，以确保处理最新的数据。




### 10.3 理解combinelatest 和zip的区别

`combineLatest` 和 `zip` 都是 Combine 中的操作符，用于将多个数据流的元素进行组合，但它们之间有重要的区别：

1. **`combineLatest` 操作符**：

   - `combineLatest` 用于将多个数据流的最新元素进行组合成一个元组，并在任一数据流发出新元素时更新输出数据流。
   - 输出的元素是由最新的各个数据流元素组成的元组，每当任一数据流的元素发生变化，都会生成新的输出元组。
   - 它适用于需要关注所有数据流的最新值的情况。

   ```swift
   let publisher1 = PassthroughSubject<Int, Never>()
   let publisher2 = PassthroughSubject<String, Never>()
   let combinedPublisher = publisher1.combineLatest(publisher2)
   ```

2. **`zip` 操作符**：

   - `zip` 用于将多个数据流的元素一一配对，只有当每个数据流都有新元素时才会发布新的元素。它会生成一系列元素对的序列。
   - 输出元素是由各个数据流的元素按顺序配对生成的，当任一数据流的元素发生变化时，才会生成新的输出元素。
   - 它适用于需要确保每个数据流的元素都有对应的值的情况。

   ```swift
   let publisher1 = [1, 2, 3].publisher
   let publisher2 = ["A", "B", "C"].publisher
   let zippedPublisher = Publishers.Zip(publisher1, publisher2)
   ```

总结区别：
- `combineLatest` 关注的是多个数据流中的最新值，一旦任一数据流的值变化，就会生成新的输出元组。
- `zip` 关注的是多个数据流的对应位置的元素，只有当每个数据流都有元素时才会生成新的输出元素。它保持了各个数据流之间的一一对应关系。

你可以根据具体的需求来选择使用 `combineLatest` 或 `zip` 操作符。如果你需要关注最新的值，并且不关心数据流之间的对应关系，可以使用 `combineLatest`。如果你需要确保数据流之间的一一对应关系，并且只关心所有数据流都有值的情况下才进行组合，可以使用 `zip`。





## 11. Time Manipulation Operators


学习各种Time Manipulation Operators
获取数据 ，统计数据，统计时间，防抖和超时等等
理解多个PUblisher之间的关系 ，熟悉发布数据的时间点概念。
理解时间操作的各种模式 ，理解使用场景。
理解DispatchQueue.main和 global概念。
理解Thread.sleep概念。


### 11.1 获取数据 ，统计数据，统计时间，防抖和超时等等

Combine 提供了一系列用于处理时间和时间相关操作的 Time Manipulation Operators（时间操纵操作符）。以下是一些常见的时间操纵操作符，以及它们的简要介绍：

1. **`delay` 操作符**：

   `delay` 操作符用于推迟数据流中元素的发布，以达到延时效果。你可以指定延时的时间间隔以及使用的调度器。

   ```swift
   let publisher = [1, 2, 3].publisher
   let delayedPublisher = publisher.delay(for: .seconds(2), scheduler: DispatchQueue.main)
   ```

2. **`debounce` 操作符**：

   `debounce` 操作符用于防抖，它会在数据流中检测元素的间隔，并只在数据流静止一段时间后才发布最新的元素。

   ```swift
   let textFieldPublisher: AnyPublisher<String, Never> = // ...
   let debouncedPublisher = textFieldPublisher
       .debounce(for: .seconds(0.5), scheduler: RunLoop.main)
   ```

3. **`throttle` 操作符**：

   `throttle` 操作符也用于控制数据流的频率，但它会定期发布最新的元素，而不管元素之间的时间间隔。

   ```swift
   let locationPublisher: AnyPublisher<Location, Never> = // ...
   let throttledPublisher = locationPublisher
       .throttle(for: .seconds(1), scheduler: DispatchQueue.global())
   ```

4. **`timeout` 操作符**：

   `timeout` 操作符用于设置一个超时时间，如果在指定的时间内没有收到数据，它会生成一个错误事件。

   ```swift
   let networkRequestPublisher: AnyPublisher<Data, Error> = // ...
   let timeoutPublisher = networkRequestPublisher
       .timeout(.seconds(10), scheduler: DispatchQueue.global())
   ```

5. **`measureInterval` 操作符**：

   `measureInterval` 操作符用于测量元素之间的时间间隔，并将时间间隔作为输出。这对于统计数据的时间间隔很有用。

   ```swift
   let dataPublisher: AnyPublisher<Int, Never> = // ...
   let intervalPublisher = dataPublisher.measureInterval(using: DispatchQueue.main)
   ```

6. **`collect` 操作符**：

   `collect` 操作符用于收集数据流中的元素，将它们分组成数组，并定期发布这些数组。这对于统计一段时间内的数据非常有用。

   ```swift
   let dataPublisher: AnyPublisher<Int, Never> = // ...
   let collectedPublisher = dataPublisher.collect(.byTimeOrCount(5, .seconds(1), scheduler: DispatchQueue.main))
   ```

这些时间操纵操作符允许你控制数据流中元素的时间特性，包括延时、防抖、超时、时间间隔测量和数据统计。你可以根据具体的需求来选择适当的操作符，以便更好地处理时间相关的数据。




### 11.2 多个PUblisher之间的关系 ，熟悉发布数据的时间点概念

在 Combine 中，多个 Publisher 之间可以存在不同的关系，这涉及到数据的发布时间点和组合方式。以下是一些常见的多个 Publisher 之间的关系以及发布数据的时间点的概念：

1. **合并（Merge）**：

   - 合并操作符（如 `merge`）用于将多个 Publisher 的元素合并成一个输出数据流，不考虑元素的顺序。发布的元素是按照它们到达的顺序发布的。
   - 无论哪个 Publisher 发出元素，都会立即发布到输出数据流中。
   - 发布数据的时间点是独立的，取决于每个 Publisher。

2. **组合（CombineLatest 和 Zip）**：

   - `combineLatest` 和 `zip` 操作符用于将多个 Publisher 的元素组合成元组或按位置对齐的元素对。
   - `combineLatest` 会在任一 Publisher 发出新元素时更新输出元组，每个元素的时间点独立。
   - `zip` 会一一对应地将多个 Publisher 的元素配对，只有当所有 Publisher 都有新元素时才会生成新的输出元素。

3. **切换（Switch To Latest）**：

   - `switchToLatest` 操作符用于处理嵌套的 Publisher，它会自动切换到最新的内部 Publisher，并在内部 Publisher 发出新元素时更新输出。
   - 发布数据的时间点取决于内部 Publisher 的时间点。

4. **合并并保持对应关系（CombineLatest）**：

   - `combineLatest` 操作符也可以用于保持多个 Publisher 之间的对应关系，将它们的最新元素组合成元组。
   - 发布数据的时间点是在任一 Publisher 发出新元素时更新输出。

5. **数据流扁平化（FlatMap 和 Switch To Latest）**：

   - `flatMap` 和 `switchToLatest` 操作符用于处理嵌套的 Publisher，将内部 Publisher 的元素扁平化成一个单一的输出数据流。
   - 发布数据的时间点取决于内部 Publisher 的时间点。

总之，多个 Publisher 之间的关系和数据发布时间点取决于所使用的操作符以及数据流的特性。你可以根据需求选择适当的操作符来实现不同的数据组合和处理方式。




### 11.3 理解时间操作的各种模式 ，理解使用场景

理解 Combine 中时间操作的各种模式以及它们的使用场景是非常重要的，因为时间操作对于异步编程和数据流处理至关重要。以下是一些常见的时间操作模式以及适用的场景：

1. **延时（Delay）**：

   - **模式**：延迟发布元素，使其在一定时间后才出现在输出数据流中。
   - **使用场景**：延时用于处理需要等待一段时间后才能处理的操作，例如在用户输入之后等待一段时间再执行搜索操作。

2. **防抖（Debounce）**：

   - **模式**：忽略一段时间内的多个元素，只保留最后一个元素。用于防止频繁的元素产生。
   - **使用场景**：防抖用于处理用户输入，以避免在用户连续输入时频繁触发操作，例如搜索建议。

3. **节流（Throttle）**：

   - **模式**：限制元素的发布速率，只发布元素的最新值，而忽略中间的元素。
   - **使用场景**：节流用于限制事件的频率，例如控制用户界面中的按钮点击或滚动事件。

4. **超时（Timeout）**：

   - **模式**：设定一个超时时间，如果在规定时间内没有接收到新元素，会生成一个错误事件。
   - **使用场景**：超时用于处理网络请求或任务的超时情况，以确保操作不会永远等待。

5. **时间间隔测量（Measure Interval）**：

   - **模式**：测量元素之间的时间间隔，并将时间间隔作为输出。
   - **使用场景**：时间间隔测量可用于监控数据的变化频率，例如监测传感器数据或计算用户活动的频率。

6. **数据统计（Collect）**：

   - **模式**：收集一定时间内的元素，并将它们分组成数组，然后定期发布这些数组。
   - **使用场景**：数据统计用于汇总一段时间内的数据，以便进行批量处理，例如在游戏中计算分数或在监测中汇总数据。

这些时间操作模式允许你在 Combine 中对时间相关的数据进行处理和控制，以适应不同的应用场景。根据具体的需求，你可以选择适当的时间操作模式来实现异步任务、事件处理和数据流控制。



### 11.4 理解DispatchQueue.main和 global概念

`DispatchQueue.main` 和 `global` 是在 Swift 中用于执行并发操作的 Dispatch 队列的两种常见类型。它们具有不同的特点和用途：

1. **DispatchQueue.main**：

   - `DispatchQueue.main` 是主队列，它在应用程序的主线程上执行任务。
   - 主队列是一个串行队列，它按照任务的添加顺序逐个执行任务。
   - 主队列通常用于执行与用户界面相关的操作，因为在主线程上更新用户界面是必需的，而主队列保证了任务的同步执行。

   示例：

   ```swift
   DispatchQueue.main.async {
       // 在主队列上执行任务，通常用于更新用户界面
   }
   ```

2. **global 队列**：

   - `global` 队列是全局并发队列，它提供了多个队列，每个队列都在不同的全局队列级别上执行任务。
   - 全局队列是并发队列，它们允许多个任务在不同线程上并行执行。
   - 全局队列通常用于执行非UI相关的后台任务，例如网络请求、数据处理等。

   示例：

   ```swift
   DispatchQueue.global(qos: .userInitiated).async {
       // 在全局队列上执行任务，通常用于后台任务
   }
   ```

`DispatchQueue.global` 接受一个 `Quality of Service (QoS)` 参数，用于指定队列的优先级。有不同级别的全局队列，如 `.userInteractive`、`.userInitiated`、`.utility` 等，用于处理不同优先级的任务。你可以根据任务的重要性和性能需求来选择合适的全局队列。

总之，`DispatchQueue.main` 用于在主线程上执行任务，通常用于更新用户界面，而 `global` 队列用于执行后台任务和其他非UI相关任务，并支持并发执行。根据任务的需求和性质，选择适当的队列来执行任务以获得最佳性能和响应性。




### 11.5 理解Thread.sleep概念

`Thread.sleep` 是一种用于在编程中暂停当前线程执行的方法。它的作用是让当前线程休眠一段时间，以模拟等待或延迟的情况。在多线程编程中，`Thread.sleep` 可能会对应用的并发性能产生不利影响，因此需要谨慎使用。

以下是关于 `Thread.sleep` 的一些关键概念：

1. **暂停当前线程**：

   当调用 `Thread.sleep` 时，它会使当前执行该代码的线程休眠一段时间。这意味着线程暂停执行，直到休眠时间结束。

2. **时间参数**：

   `Thread.sleep` 接受一个时间参数，通常以毫秒（milliseconds）为单位。这个参数表示线程休眠的时间长度。例如，`Thread.sleep(1000)` 表示线程休眠 1000 毫秒（1 秒）。

3. **阻塞**：

   在 `Thread.sleep` 的执行期间，线程会进入阻塞状态，这意味着它不会占用 CPU 时间，从而释放 CPU 资源供其他线程使用。这对于减轻 CPU 负载是有益的。

4. **谨慎使用**：

   在多线程编程中，过度使用 `Thread.sleep` 可能会导致性能问题和竞争条件。因为它会直接暂停线程的执行，而不会考虑线程的状态或资源需求，因此可能会引发不可预测的问题。通常更好的做法是使用线程同步机制、条件变量或定时器来等待特定条件的发生。

5. **异常处理**：

   在使用 `Thread.sleep` 时，应注意处理可能的异常，因为线程休眠时间过长可能导致中断异常。在 Java 中，这可能是 `InterruptedException`。

示例（Java）：

```java
try {
    // 休眠 2 秒
    Thread.sleep(2000);
} catch (InterruptedException e) {
    // 处理中断异常
}
```

总之，`Thread.sleep` 是一种在编程中用于暂停线程执行的机制，但它应当谨慎使用，避免对应用的性能和响应性产生不利影响。在多线程编程中，通常更好的做法是使用更高级的同步和等待机制，以更精确地控制线程的行为。





## 12. SequenceOperators


学习各种SeauenceOperators
 min, max, first, last, output, contains,statisfyAll, reduce
min:by理解数值比较和逻辑比较的区别。
理解Comparable，并且实现这个协议。
理解reduce概念。
理解各个SequenceOperators 的参数，避免没有必要的开发。


### 12.1 常用的操作符min, max, first, last, output, contains,statisfyAll, reduce

Combine 框架提供了一系列 Sequence Operators（序列操作符）来处理数据流中的元素。下面是一些常见的 Sequence Operators 以及它们的简要介绍：

1. **`min` 和 `max` 操作符**：

   - `min` 用于找到数据流中的最小元素，`max` 用于找到最大元素。
   - 这些操作符返回一个 Future，将在数据流完成时发布最小或最大的元素。

   示例：

   ```swift
   let numbers = [5, 2, 8, 1, 6]
   let minNumber = numbers.publisher.min()
   let maxNumber = numbers.publisher.max()
   ```

2. **`first` 和 `last` 操作符**：

   - `first` 用于找到数据流中的第一个元素，`last` 用于找到最后一个元素。
   - 这些操作符返回一个 Future，将在数据流完成时发布相应的元素。

   示例：

   ```swift
   let numbers = [5, 2, 8, 1, 6]
   let firstNumber = numbers.publisher.first()
   let lastNumber = numbers.publisher.last()
   ```

3. **`output` 操作符**：

   - `output` 用于从数据流中提取某个特定位置的元素，类似于数组的 subscript。
   - 这个操作符接受一个索引值，返回一个 Future，将在数据流完成时发布该索引位置的元素。

   示例：

   ```swift
   let numbers = [5, 2, 8, 1, 6]
   let thirdNumber = numbers.publisher.output(at: 2)
   ```

4. **`contains` 操作符**：

   - `contains` 用于检查数据流是否包含某个特定元素。
   - 这个操作符返回一个 Future，将在数据流完成时发布包含结果（true 或 false）。

   示例：

   ```swift
   let fruits = ["apple", "banana", "cherry"]
   let containsBanana = fruits.publisher.contains("banana")
   ```

5. **`satisfyAll` 操作符**：

   - `satisfyAll` 用于检查数据流中的所有元素是否都满足某个特定条件。
   - 这个操作符返回一个 Future，将在数据流完成时发布布尔值，表示是否所有元素都满足条件。

   示例：

   ```swift
   let numbers = [5, 2, 8, 1, 6]
   let allEven = numbers.publisher.allSatisfy { $0 % 2 == 0 }
   ```

6. **`reduce` 操作符**：

   - `reduce` 用于将数据流中的元素进行累积操作，返回一个结果。
   - 这个操作符接受一个初始值和一个闭包，将数据流中的元素与初始值进行累积操作，并返回最终结果。

   示例：

   ```swift
   let numbers = [5, 2, 8, 1, 6]
   let sum = numbers.publisher.reduce(0) { $0 + $1 }
   ```

这些 Sequence Operators 允许你对数据流中的元素进行各种操作，包括查找最小/最大值、获取第一个/最后一个元素、检查是否包含某个元素、检查是否满足特定条件，以及进行累积操作。你可以根据需要选择适当的操作符来处理数据流中的元素。




### 12.2 min:by理解数值比较和逻辑比较的区别

`min` 操作符在 Combine 中有两种变体，分别是 `min(by:)` 和 `min()`. 这两种变体用于找到数据流中的最小元素，但它们的比较方式略有不同。

1. **`min()` 操作符**：

   - `min()` 操作符用于查找数据流中的最小元素，该元素必须是 `Comparable` 类型，因为它使用标准的逻辑比较操作符进行比较。
   - 这意味着如果元素是 `Int`、`Double`、`String` 或其他遵循 `Comparable` 协议的类型，可以直接使用 `min()` 进行比较。
   - `min()` 返回一个 `Publisher`，当数据流完成时发布最小的元素。

   示例：

   ```swift
   let numbers = [5, 2, 8, 1, 6]
   let minNumber = numbers.publisher.min()
   ```

2. **`min(by:)` 操作符**：

   - `min(by:)` 操作符允许你自定义比较的逻辑，因为它接受一个闭包作为参数，该闭包定义了元素之间的比较方式。
   - 这使得你可以使用自定义的比较逻辑来查找最小元素，而不仅仅依赖于元素的 `Comparable` 实现。
   - `min(by:)` 返回一个 `Publisher`，当数据流完成时发布符合自定义比较逻辑的最小元素。

   示例：

   ```swift
   let products = [
       Product(name: "Apple", price: 1.0),
       Product(name: "Banana", price: 0.5),
       Product(name: "Cherry", price: 1.5)
   ]
   let cheapestProduct = products.publisher.min(by: { $0.price < $1.price })
   ```

总结：
- `min()` 使用标准的逻辑比较操作符，适用于遵循 `Comparable` 协议的元素。
- `min(by:)` 允许你定义自定义的比较逻辑，适用于不遵循 `Comparable` 协议的元素或需要特定的比较方式的情况。




### 12.3 理解Comparable，并且实现这个协议

`Comparable` 是 Swift 标准库中的一个协议，用于定义可以进行比较的数据类型。遵循 `Comparable` 协议的类型可以使用标准的比较运算符（如 `<`、`<=`、`>`、`>=`）来进行比较操作，以确定它们的相对顺序。

`Comparable` 协议要求实现两个方法：

1. **`<` 操作符**：用于比较两个值，如果调用者小于另一个值，则返回 `true`；否则返回 `false`。

2. **`==` 操作符**：用于检查两个值是否相等。这个方法通常是由协议的默认实现提供的，但也可以自定义。

以下是一个示例，演示如何定义一个遵循 `Comparable` 协议的自定义类型：

```swift
struct Person: Comparable {
    var name: String
    var age: Int

    static func < (lhs: Person, rhs: Person) -> Bool {
        return lhs.age < rhs.age
    }

    static func == (lhs: Person, rhs: Person) -> Bool {
        return lhs.name == rhs.name && lhs.age == rhs.age
    }
}

let person1 = Person(name: "Alice", age: 30)
let person2 = Person(name: "Bob", age: 25)

if person1 < person2 {
    print("\(person1.name) is younger than \(person2.name)")
} else {
    print("\(person1.name) is older than or equal to \(person2.name)")
}
```

在上述示例中，`Person` 结构体遵循 `Comparable` 协议，并实现了 `<` 和 `==` 操作符。这使得我们可以使用 `<` 运算符来比较两个 `Person` 对象的年龄，并使用 `==` 运算符来检查它们是否具有相同的名称和年龄。

通过实现 `Comparable` 协议，你可以定义自己的自定义类型，使它们具有比较功能，以便进行排序和其他比较操作。这对于处理需要比较的数据结构非常有用。



### 12.4 理解各个SequenceOperators 的参数，避免没有必要的开销

了解各个 Sequence Operators 的参数是很重要的，因为它们的参数可以影响操作的行为和结果。避免不必要的开销和错误使用是使用这些操作符的关键。以下是一些常见 Sequence Operators 的参数以及如何避免不必要的开销：

1. **`min` 和 `max` 操作符**：

   - 参数：这些操作符通常不需要额外参数，它们会使用数据流中的元素的默认比较方式来找到最小或最大元素。
   - 避免不必要的开销：确保数据流中的元素是 `Comparable` 类型，并且你不需要自定义比较逻辑。

2. **`output` 操作符**：

   - 参数：这个操作符需要一个索引值作为参数，用于提取数据流中的特定位置的元素。
   - 避免不必要的开销：确保指定的索引值在数据流中有效，避免越界访问。

3. **`contains` 操作符**：

   - 参数：这个操作符需要一个要查找的元素作为参数。
   - 避免不必要的开销：确保要查找的元素是数据流中的合法元素，避免不必要的查找。

4. **`satisfyAll` 操作符**：

   - 参数：这个操作符需要一个闭包，用于定义要满足的条件。
   - 避免不必要的开销：确保闭包的条件是正确的，不会导致不必要的计算。

5. **`reduce` 操作符**：

   - 参数：这个操作符需要一个初始值和一个闭包，用于执行累积操作。
   - 避免不必要的开销：确保初始值和累积操作是正确的，不会导致不必要的计算。

6. **其他操作符**：

   - 不同的操作符具有不同的参数，包括闭包、初始值、谓词等。避免不必要的开销的关键是正确理解操作符的参数，并确保它们满足你的需求。

总之，理解每个 Sequence Operator 的参数是使用 Combine 操作符的关键。确保参数正确设置，并避免不必要的开销，以获得有效的数据流处理。根据需要仔细查阅操作符的文档以了解其参数和使用方式。




## 13. Debug


学习Cimbine中提供的DeabugOperator
print ,print(:to), breakpoint, breakpointOn Error
breakpoint理解各个参数。
关于Debug重点，还是在于处理流程的理解，在此基础上进行数据的监控。


### 13.1 常用的DeabuaOperator，print ,print(:to), breakpoint, breakpointOn Error

Combine 框架提供了一些调试操作符，用于帮助开发者更容易地调试 Combine 数据流。这些操作符可以用于在 Combine 数据流的不同步骤中输出信息、设置断点，以及在错误发生时执行特定的调试操作。以下是其中一些调试操作符：

1. **`print` 操作符**：

   - `print` 操作符用于在数据流的不同点打印信息，以便调试。
   - 它接受一个标签和一个输出样式，用于自定义打印的格式。

   示例：

   ```swift
   dataPublisher
       .print("Debug Data")
       .sink { value in
           print("Received value: \(value)")
       }
   ```

2. **`print(_:_:)` 操作符**：

   - `print(_:to:)` 操作符与 `print` 操作符类似，但它可以将输出发送到指定的输出流，例如控制台或日志文件。

   示例：

   ```swift
   dataPublisher
       .print("Debug Data", to: &logger)
       .sink { value in
           print("Received value: \(value)")
       }
   ```

3. **`breakpoint` 操作符**：

   - `breakpoint` 操作符用于在数据流的特定点设置断点，以便在这里暂停调试。
   - 它可以用于在数据流的特定步骤中进行检查。

   示例：

   ```swift
   dataPublisher
       .breakpoint()
       .sink { value in
           print("Received value: \(value)")
       }
   ```

4. **`breakpointOnError` 操作符**：

   - `breakpointOnError` 操作符与 `breakpoint` 操作符类似，但它仅在错误发生时设置断点。

   示例：

   ```swift
   dataPublisher
       .breakpointOnError()
       .sink { value in
           print("Received value: \(value)")
       }
   ```

这些调试操作符可以帮助你更轻松地诊断 Combine 数据流中的问题，包括查看数据流中的值、设置断点以便在特定点进行调试，以及在错误发生时暂停调试。它们在开发和调试期间非常有用，但在生产代码中通常不建议使用。




### 13.2 breakpoint理解各个参数。

`breakpoint` 操作符是 Combine 框架提供的一种调试工具，用于在数据流的特定点设置断点，以便在这里暂停调试。`breakpoint` 操作符有几个参数，让你可以指定在何时触发断点以及触发断点时的行为。以下是 `breakpoint` 操作符的参数：

1. **`name`（参数标签：name）**：

   - `name` 是一个可选的字符串参数，用于为断点设置一个名称。这个名称会显示在 Xcode 的调试器中，以便你更容易地识别断点的目的。

   示例：

   ```swift
   dataPublisher
       .breakpoint(name: "Custom Breakpoint")
       .sink { value in
           print("Received value: \(value)")
       }
   ```

2. **`condition`（参数标签：condition）**：

   - `condition` 是一个可选的闭包，它定义了触发断点的条件。只有当该闭包返回 `true` 时，断点才会触发。
   - 该闭包接受数据流中的元素作为参数，你可以根据这些元素定义触发条件。

   示例：

   ```swift
   dataPublisher
       .breakpoint(condition: { value in
           return value > 10
       })
       .sink { value in
           print("Received value: \(value)")
       }
   ```

3. **`action`（参数标签：action）**：

   - `action` 是一个可选的参数，定义了触发断点时执行的操作。它接受一个参数，表示触发断点的数据流元素，以便你可以执行自定义操作。

   示例：

   ```swift
   dataPublisher
       .breakpoint(action: { value in
           print("Custom action for value: \(value)")
       })
       .sink { value in
           print("Received value: \(value)")
       }
   ```

使用这些参数，你可以根据需要自定义断点的名称、触发条件和触发时的操作。这使得 `breakpoint` 操作符成为了一个强大的调试工具，可用于更精细地控制何时和如何在数据流中设置断点，以便更轻松地调试和诊断问题。不过，在生产代码中通常不建议保留 `breakpoint` 操作符，因为它主要用于开发和调试阶段。




### 13.3 关于Debug重点，还是在于处理流程的理解，在此基础上进行数据的监控

对于 Combine 中的调试，确实重点在于理解数据流的处理流程以及在此基础上进行数据的监控和诊断。以下是一些关键方面，可以帮助你更好地理解和处理 Combine 数据流的调试过程：

1. **数据流的处理流程**：

   在使用 Combine 操作符时，首要任务是理解数据流的处理流程。了解数据是如何从发布者到订阅者传递的，以及中间经过的操作符如何转换和处理数据，是非常重要的。这有助于你明确每个步骤的作用和顺序。

2. **调试输出**：

   Combine 提供了一系列用于输出调试信息的操作符，如 `print` 和 `breakpoint`。这些操作符允许你在数据流的不同点输出信息，以查看数据流的中间状态。通过输出关键信息，你可以更好地理解数据流的处理过程。

3. **断点设置**：

   使用 `breakpoint` 操作符可以在数据流的特定点设置断点。这对于在特定条件下触发断点以进行详细调试非常有用。你可以指定触发断点的条件和触发时执行的操作，以精确控制断点的行为。

4. **错误处理**：

   在数据流中处理错误也是一个重要的调试方面。Combine 提供了处理错误的操作符，如 `catch` 和 `replaceError`。正确处理错误并输出相关信息有助于快速诊断问题。

5. **数据监控**：

   了解数据流中的数据是如何变化的，以及观察数据流中的元素和值的变化是重要的。可以使用输出操作符和订阅操作符来监控数据的变化。

6. **调试工具**：

   Xcode 提供了强大的调试工具，如调试器和控制台，用于监控和诊断 Combine 数据流。你可以在调试器中查看数据流的状态，检查变量的值，设置断点等。

总的来说，调试 Combine 数据流的关键在于理解数据流的处理流程和每个操作符的作用，以及合理使用调试工具和操作符来监控数据的变化和诊断问题。这有助于更快地发现和解决潜在的错误和问题。





## 14. Error Handling

学习Combine中提供的ErrorOperator
setFailureType, tryMap, mapError, replace Error, retry
mapError, setFailure和retry的工作流程。
能够熟练使用以上的知识，来处理Cornbine中出现的错误逻辑


### 14.1 常用的ErrorOperator，setFailureType, tryMap, mapError, replace Error, retry

Combine 提供了多种错误处理操作符，用于处理数据流中可能发生的错误。以下是一些常用的错误操作符：

1. **`setFailureType` 操作符**：

   - `setFailureType` 操作符用于更改数据流的错误类型。这对于将特定错误类型转换为其他类型或限制错误类型非常有用。

   示例：

   ```swift
   dataPublisher
       .setFailureType(to: CustomError.self)
       .sink(receiveCompletion: { completion in
           switch completion {
           case .failure(let error):
               print("Received custom error: \(error)")
           case .finished:
               print("Data stream completed")
           }
       }, receiveValue: { value in
           // Handle data
       })
   ```

2. **`tryMap` 操作符**：

   - `tryMap` 操作符用于在数据流的处理过程中对元素进行转换，同时可以处理可能引发错误的转换操作。

   示例：

   ```swift
   dataPublisher
       .tryMap { data in
           guard data.isValid else {
               throw DataError.invalidData
           }
           return data.processedValue
       }
       .sink(receiveCompletion: { completion in
           // Handle completion
       }, receiveValue: { value in
           // Handle valid processed value
       })
   ```

3. **`mapError` 操作符**：

   - `mapError` 操作符用于将错误类型进行转换，以便在错误处理时使用不同的错误类型。

   示例：

   ```swift
   dataPublisher
       .mapError { originalError in
           return CustomError.convertedError(originalError)
       }
       .sink(receiveCompletion: { completion in
           switch completion {
           case .failure(let error):
               print("Received custom error: \(error)")
           case .finished:
               print("Data stream completed")
           }
       }, receiveValue: { value in
           // Handle data
       })
   ```

4. **`replaceError` 操作符**：

   - `replaceError` 操作符用于在发生错误时替换为默认值或其他元素，从而允许数据流继续。

   示例：

   ```swift
   dataPublisher
       .replaceError(with: defaultValue)
       .sink(receiveCompletion: { completion in
           // Handle completion
       }, receiveValue: { value in
           // Handle data or default value
       })
   ```

5. **`retry` 操作符**：

   - `retry` 操作符用于在发生错误时尝试重新订阅数据流，以便数据流可以继续。你可以指定重试的次数或条件。

   示例：

   ```swift
   dataPublisher
       .retry(3) // 尝试重试3次
       .sink(receiveCompletion: { completion in
           // Handle completion
       }, receiveValue: { value in
           // Handle data
       })
   ```

这些错误操作符可以帮助你更好地处理数据流中的错误，以及根据需要执行转换、替换、重试等操作，以保持数据流的稳定性和可靠性。根据具体的业务需求和错误情况，选择适当的错误操作符来处理错误非常重要。




### 14.2 mapError, setFailure和retry的工作流程

让我们分别讨论 `mapError`、`setFailureType` 和 `retry` 操作符的工作流程：

1. **`mapError` 操作符**：

   - `mapError` 操作符用于将数据流中的错误类型进行转换。它接受一个闭包，该闭包接受原始错误类型并返回转换后的错误类型。
   - 当数据流中发生错误时，`mapError` 会应用闭包来转换错误类型，然后将转换后的错误类型传递给下游的订阅者。
   - 如果转换成功，数据流将继续传递。

   示例：

   ```swift
   dataPublisher
       .mapError { originalError in
           return CustomError.convertedError(originalError)
       }
       .sink(receiveCompletion: { completion in
           switch completion {
           case .failure(let error):
               print("Received custom error: \(error)")
           case .finished:
               print("Data stream completed")
           }
       }, receiveValue: { value in
           // Handle data
       })
   ```

2. **`setFailureType` 操作符**：

   - `setFailureType` 操作符用于更改数据流的错误类型。它接受一个新的错误类型，并将数据流的错误类型更改为指定的类型。
   - 当数据流中发生错误时，`setFailureType` 会将错误类型更改为指定的类型，然后将转换后的错误类型传递给下游的订阅者。
   - 如果转换成功，数据流将继续传递。

   示例：

   ```swift
   dataPublisher
       .setFailureType(to: CustomError.self)
       .sink(receiveCompletion: { completion in
           switch completion {
           case .failure(let error):
               print("Received custom error: \(error)")
           case .finished:
               print("Data stream completed")
           }
       }, receiveValue: { value in
           // Handle data
       })
   ```

3. **`retry` 操作符**：

   - `retry` 操作符用于在发生错误时尝试重新订阅数据流，以便数据流可以继续。
   - 当数据流中发生错误时，`retry` 操作符会尝试重新订阅数据流，允许数据流重新执行。
   - 你可以指定重试的次数或条件，以控制重试行为。

   示例：

   ```swift
   dataPublisher
       .retry(3) // 尝试重试3次
       .sink(receiveCompletion: { completion in
           // Handle completion
       }, receiveValue: { value in
           // Handle data
       })
   ```

总的来说，这些操作符的工作流程是在数据流中发生错误时进行干预。`mapError` 和 `setFailureType` 用于转换或更改错误类型，以便订阅者可以处理特定类型的错误。`retry` 用于在发生错误时尝试重新订阅数据流，以保持数据流的连续性。根据需要，你可以组合使用这些操作符来处理和恢复数据流中的错误情况。





## 15. Callback和 Future

Swift中闭包closure的定义，以及其特点。
引1用计数【ARC】。
combine中提供的Future。
相同的异步业务，如何用callback和Future实现。
体会两个实现的方法。
理解callback和Future的实现互相转化。
从调用接口，避免循环强引1用，执行上下文，执行线程等方面考虑。



### 15.1 Swift中闭包closure的定义，以及其特点

闭包（Closure）是一种在 Swift 中定义和使用的自包含函数块，它捕获并存储了其周围上下文中的常量和变量引用。闭包在 Swift 中具有以下特点：

1. **自包含性**：闭包是自包含的，它包含了代码块和其引用的数据，因此它可以在需要时被传递、存储和执行，而无需依赖于外部数据或函数。

2. **函数体**：闭包包含一个函数体，可以接受参数和返回值。函数体中可以包含一段或多段代码，用于执行特定的任务或操作。

3. **捕获值**：闭包可以捕获和存储在其周围上下文中定义的常量和变量引用，以便在闭包执行时访问这些值。这使得闭包可以"捕获"外部上下文中的数据，使其在闭包内可用。

4. **无需函数名**：闭包可以在没有函数名的情况下被定义和使用，使其非常灵活。

5. **参数和返回值**：闭包可以接受参数和返回值。参数允许你向闭包传递数据，返回值允许闭包将结果返回给调用方。

6. **语法简洁**：Swift 提供了简洁的语法来定义闭包，包括简化的参数和返回值声明。

在 Swift 中，有三种主要类型的闭包：

1. **全局函数**：这是在全局作用域中定义的普通函数，可以被其他代码调用。它们是最基本的闭包类型。

2. **嵌套函数**：这些是在函数内部定义的函数，通常用于封装和隐藏特定任务的实现细节。嵌套函数可以访问外部函数的参数和变量。

3. **闭包表达式**：这是一种使用简洁语法定义的匿名函数，也称为匿名闭包。它们可以被传递给函数、存储在变量中，以及作为参数传递给其他函数。

闭包在 Swift 中用于处理许多编程任务，包括排序、筛选、映射、异步编程和事件处理等。它们是 Swift 中的强大工具，能够使代码更灵活、可读性更高，并能够实现函数式编程的特性。



### 15.2 引1用计数【ARC】

引用计数（Reference Counting）是一种内存管理技术，用于自动跟踪和管理对象在内存中的生命周期。在引用计数中，每个对象都有一个与之相关联的引用计数，它表示了有多少个指向该对象的引用。当引用计数为零时，对象会被释放，即从内存中移除。

Swift 中使用引用计数自动引用计数（Automatic Reference Counting，ARC）来管理内存。ARC 会自动为你追踪对象的引用，并在不再需要的时候释放内存，以避免内存泄漏。

以下是引用计数（ARC）的一些关键概念：

1. **引用计数**：每个对象都有一个引用计数，表示有多少个引用指向该对象。当引用计数为零时，对象将被释放。

2. **引用计数增加**：当新的引用指向对象时，引用计数会增加。这发生在对象被分配给变量、数组、字典、或者通过函数参数传递时。

3. **引用计数减少**：当引用不再指向对象时，引用计数会减少。这发生在引用离开作用域、被重新分配、或者从集合中移除时。

4. **循环引用**：循环引用是指两个或多个对象互相引用，导致它们的引用计数永远不会为零，从而导致内存泄漏。Swift 使用强引用和弱引用来处理循环引用问题。

5. **强引用**：默认情况下，Swift 中的引用都是强引用。强引用会增加对象的引用计数，只有当所有强引用离开作用域时，对象的引用计数才会减少。

6. **弱引用**：弱引用不会增加对象的引用计数。当对象只有弱引用时，引用计数为零时对象会被释放。这有助于解决循环引用问题。

7. **无主引用**：无主引用类似于弱引用，但与弱引用不同，无主引用通常假定对象不会被释放。它适用于被期望在整个对象的生命周期内都存在的情况。

Swift 的引用计数是基于 ARC 的自动管理，大部分情况下你无需手动管理对象的内存。Swift 会自动插入引用计数增加和减少的代码，以确保对象的内存管理是正确的。这使得 Swift 在内存管理方面更加安全和高效。



### 15.3 combine中提供的Future

在 Combine 框架中，`Future` 是一种发布者（Publisher），它表示将来会产生一个值或错误。`Future` 可以用于表示异步操作的结果，而不需要手动处理回调闭包。它在 Combine 中非常有用，因为它允许你将异步操作封装为 Combine 发布者，从而可以轻松地与其他发布者进行组合和处理。

以下是使用 `Future` 发布者的示例：

```swift
import Combine

enum CustomError: Error {
    case someError
}

func performAsyncOperation() -> Future<String, Error> {
    return Future { promise in
        // 模拟异步操作
        DispatchQueue.global().async {
            // 假设异步操作成功
            let result = "Async operation result"
            
            // 完成时，调用 promise 来产生值
            promise(.success(result))
        }
    }
}

// 订阅 Future 发布者
let cancellable = performAsyncOperation()
    .sink(receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Future operation completed.")
        case .failure(let error):
            print("Error: \(error)")
        }
    }, receiveValue: { value in
        print("Received value: \(value)")
    })
```

在上面的示例中，`performAsyncOperation` 函数返回一个 `Future` 发布者，该发布者表示一个将来可能产生的字符串值或错误。在闭包中，异步操作完成后，使用 `promise` 参数来发出结果或错误。然后，我们使用 `sink` 订阅该发布者，以处理异步操作的结果或错误。

`Future` 发布者是一种强大的工具，可用于将异步操作集成到 Combine 数据流中，以便更容易地处理和组合异步操作的结果。它使得异步代码的使用更加简单和可读，同时避免了回调地狱的情况。



### 15.4 相同的异步业务，如何用callback和Future实现

你可以使用回调（callback）和 `Future` 来实现相同的异步业务。下面是一个示例，演示如何分别使用回调和 `Future` 来执行相同的异步操作。在这个示例中，我们将模拟下载文件的异步操作。

使用回调（Callback）：

```swift
import Foundation

enum CustomError: Error {
    case downloadFailed
}

func downloadFileWithCallback(completion: @escaping (Result<String, Error>) -> Void) {
    DispatchQueue.global().async {
        // 模拟异步下载操作
        if Bool.random() {
            completion(.success("Downloaded file"))
        } else {
            completion(.failure(CustomError.downloadFailed))
        }
    }
}

downloadFileWithCallback { result in
    switch result {
    case .success(let file):
        print("Downloaded file: \(file)")
    case .failure(let error):
        print("Download error: \(error)")
    }
}
```

使用 `Future`：

```swift
import Combine

func downloadFileWithFuture() -> Future<String, Error> {
    return Future { promise in
        DispatchQueue.global().async {
            // 模拟异步下载操作
            if Bool.random() {
                promise(.success("Downloaded file"))
            } else {
                promise(.failure(CustomError.downloadFailed))
            }
        }
    }
}

let cancellable = downloadFileWithFuture()
    .sink(receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Download completed")
        case .failure(let error):
            print("Download error: \(error)")
        }
    }, receiveValue: { file in
        print("Downloaded file: \(file)")
    })
```

这两种方法都可以用来执行相同的异步操作，但它们的工作方式略有不同。回调方法使用闭包作为参数，当操作完成时，调用闭包并传递结果。`Future` 方法则将异步操作封装为一个发布者，通过调用 `promise` 方法来传递结果。你可以根据需求选择使用哪种方法，但使用 `Future` 可以更容易地集成到 Combine 数据流中，从而实现更复杂的异步操作处理和组合。



### 15.5 理解callback和Future的实现互相转化
从调用接口，避免循环强引1用，执行上下文，执行线程等方面考虑

在某些情况下，你可能需要在使用回调和使用 `Future` 之间进行互相转化，以便在不同的代码块之间传递数据或执行异步操作。下面是一些关于如何进行转化和一些注意事项的示例：

**从回调到 Future 转化**：

```swift
import Combine

func convertCallbackToFuture() -> Future<String, Error> {
    return Future { promise in
        // 调用使用回调的异步函数
        downloadFileWithCallback { result in
            switch result {
            case .success(let file):
                promise(.success(file))
            case .failure(let error):
                promise(.failure(error))
            }
        }
    }
}

let cancellable = convertCallbackToFuture()
    .sink(receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Download completed")
        case .failure(let error):
            print("Download error: \(error)")
        }
    }, receiveValue: { file in
        print("Downloaded file: \(file)")
    })
```

在这个示例中，我们创建了一个名为 `convertCallbackToFuture` 的函数，该函数返回一个 `Future` 发布者，通过调用使用回调的异步函数并在回调中将结果传递给 `promise` 来实现转化。这样可以在 Combine 流中使用异步操作的结果。

**从 Future 到回调转化**：

```swift
func convertFutureToCallback(completion: @escaping (Result<String, Error>) -> Void) {
    downloadFileWithFuture()
        .sink(receiveCompletion: { completion in
            // 处理 Combine 发布者的完成状态
            switch completion {
            case .finished:
                // 如果成功完成，不执行回调
                break
            case .failure(let error):
                completion(.failure(error))
            }
        }, receiveValue: { file in
            completion(.success(file))
        })
        .store(in: &cancellables)
}

// 调用转化后的回调函数
convertFutureToCallback { result in
    switch result {
    case .success(let file):
        print("Downloaded file: \(file)")
    case .failure(let error):
        print("Download error: \(error)")
    }
}
```

在这个示例中，我们创建了一个名为 `convertFutureToCallback` 的函数，该函数接受一个回调闭包作为参数。在函数内部，我们使用 `sink` 订阅 `Future` 发布者，然后根据发布者的完成状态将结果传递给回调闭包。

在转化时需要注意以下几点：

1. 异步操作的执行上下文和线程可能会因转化而改变。在从回调转化为 `Future` 时，确保在 `Future` 的闭包中采取适当的线程管理措施，以确保在合适的上下文中执行异步操作。同样，在从 `Future` 转化为回调时，也要考虑执行上下文。

2. 避免循环强引用问题。在从 `Future` 转化为回调时，确保不会出现循环强引用，否则可能导致内存泄漏。

3. 考虑异常处理。在将结果传递给回调时，需要确保将错误信息传递给回调，以便在出现错误时能够处理异常情况。

这些示例说明了如何在回调和 `Future` 之间进行转化，并提供了一些注意事项来处理线程和异常情况。根据实际需求和代码结构，你可以选择合适的方法来实现转化。




## 16. Network Layer

使用Postman进行简单的mock WebApi.
设计简单的WebApi接口。
了解和使用 URLSession的data TaskPublisher扩展。
理解实现的程序结构。

### 16.1 了解和使用 URLSession的data TaskPublisher扩展

`URLSession` 的 `dataTaskPublisher(for:)` 方法是 Combine 框架中的扩展，用于将 `URLSessionDataTask` 转化为 Combine 的发布者（Publisher）。这允许你使用 Combine 的功能来处理网络请求和响应数据。

以下是如何使用 `dataTaskPublisher(for:)` 执行网络请求并处理响应数据的示例：

```swift
import SwiftUI
import Combine

struct ContentView: View {
    @State private var data: Data?
    @State private var error: Error?
    
    private var cancellables = Set<AnyCancellable>()
    
    var body: some View {
        VStack {
            Text("Network Request Example")
                .font(.title)
            
            if let data = data {
                Text("Data received:")
                Text(String(data: data, encoding: .utf8) ?? "Unable to decode data")
            }
            
            if let error = error {
                Text("Error: \(error.localizedDescription)")
            }
            
            Button("Fetch Data") {
                fetchData()
            }
        }
    }
    
    func fetchData() {
        guard let url = URL(string: "https://jsonplaceholder.typicode.com/posts/1") else {
            return
        }
        
        URLSession.shared.dataTaskPublisher(for: url)
            .map(\.data)
            .receive(on: DispatchQueue.main)
            .sink(receiveCompletion: { completion in
                switch completion {
                case .finished:
                    break
                case .failure(let networkError):
                    self.error = networkError
                }
            }, receiveValue: { receivedData in
                self.data = receivedData
            })
            .store(in: &cancellables)
    }
}

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

在这个示例中，我们首先定义了一个 `ContentView`，其中包含了一个按钮，当按钮被点击时，它会执行 `fetchData` 方法来发起网络请求。

在 `fetchData` 方法中，我们使用 `URLSession.shared.dataTaskPublisher(for:)` 来创建一个 Combine 发布者，该发布者执行网络请求并返回响应数据。然后，我们使用 `.map(\.data)` 来提取数据部分，接着使用 `.receive(on: DispatchQueue.main)` 切换到主线程以更新界面。

最后，我们使用 `.sink` 订阅该发布者，以处理网络请求的完成状态和响应数据。成功时，我们将数据存储到 `data` 属性中，失败时，我们将错误信息存储到 `error` 属性中。

这样，你可以使用 `dataTaskPublisher(for:)` 方法来执行网络请求，并将其与 Combine 进行集成，以处理异步操作的结果和更新用户界面。




## 17. Key-Value监视和@Published注解

Obiective-C的NSObiect @obic dynamic 属性，也是发布者Publisher.
理解object.publisher(for:,options)参数。
理解Publisher 的扩展
`public func assign<Root>(to kexPath: Reference WritableKeyPath<Root, Self Outputs, on object: Root) -> Anycancellable`
ObservableObject的@Published属性是 Publisher.
理解 Publisher 的扩展
`public func assign(to published: inout Published<Self Output>.Publisher).`
熟悉Key-Valve 监视的接口后，可以很方便地应用的项目中。


### 17.1 Obiective-C的NSObiect @obic dynamic 属性，也是发布者Publisher

在 Objective-C 中，`NSObject` 的 `@property` 属性可以使用 `@dynamic` 关键字来声明为动态属性，这意味着属性的 getter 和 setter 方法由运行时动态生成，而不是在编译时由编译器生成。这种方式允许你自定义属性的访问和设置行为，包括在属性被访问或设置时触发其他操作，例如发布者-订阅者（Publisher-Subscriber）模式。

虽然 Objective-C 不直接提供 Combine 框架，但你可以通过自定义动态属性的 getter 和 setter 方法来实现发布者模式。以下是一个示例，演示如何在 Objective-C 中实现一个简单的发布者：

```objective-c
#import <Foundation/Foundation.h>

// 自定义发布者
@interface CustomPublisher : NSObject

// 动态属性
@property (nonatomic, strong) NSString *message;

@end

@implementation CustomPublisher

// 自定义发布者的setter方法
- (void)setMessage:(NSString *)message {
    _message = message;
    
    // 当属性被设置时，通知订阅者（发布消息）
    [[NSNotificationCenter defaultCenter] postNotificationName:@"CustomPublisherMessageUpdated" object:self userInfo:@{@"message": message}];
}

@end
```

在上面的示例中，我们创建了一个名为 `CustomPublisher` 的类，它具有一个动态属性 `message`。当 `message` 属性被设置时，我们在 setter 方法中使用 `NSNotificationCenter` 发送通知，通知订阅者（观察者）属性的变化。

这种方式可以用于实现基本的发布者-订阅者模式，但请注意，Combine 框架在 Swift 中提供了更强大的工具来处理数据流和异步操作。如果你正在编写新的 Swift 代码，建议考虑使用 Combine 框架，它提供了专门的发布者和操作符来管理数据流、异步操作和事件处理。



### 17.2 object.publisher(for:,options)参数

在 Swift 中，`object.publisher(for:keyPath:options:)` 是 `NSObject` 的 Combine 扩展方法，它用于创建一个 Combine 发布者，以监视指定键路径的属性变化。这个方法的参数如下：

- `keyPath`：一个字符串，表示要监视的属性的键路径。键路径是一个描述属性的访问路径的字符串，通常使用点号分隔属性和嵌套的属性。例如，如果你要监视一个对象的 `name` 属性，你可以传递键路径 "name"。

- `options`：一个可选的选项参数，它是一个整数，表示如何监视属性的变化。你可以使用 Combine 提供的常量值来设置不同的选项。一些常见的选项包括：
  - `.new`：表示要包含属性的新值。
  - `.old`：表示要包含属性的旧值。
  - `.initial`：表示要在订阅时立即发送当前属性值。
  - `.prior`：表示要在属性值变化之前发送通知。

使用 `object.publisher(for:keyPath:options:)` 方法时，你可以传递适当的 `keyPath` 和 `options` 参数，以获取你感兴趣的属性变化的发布者。一旦订阅了这个发布者，你可以接收属性变化的事件，并在 Combine 数据流中处理它们。

这个方法在 Swift 中是非常有用的，因为它允许你以响应式的方式监视和处理属性的变化，而无需手动实现键-值观察（KVO）模式的回调方法。这使得属性变化的处理更加简洁和直观。


### 17.3 Publisher 的扩展 `public func assign<Root>(to kexPath: Reference WritableKeyPath<Root, Self Outputs, on object: Root) -> AnyCancellable`

`assign(to:on:)` 是 Combine 框架中的一种扩展方法，它用于将 Combine 发布者的输出值赋值给指定对象的可写属性，以便在属性的值发生变化时反映发布者的输出值。这个方法的参数解释如下：

- `keyPath`：这是一个键路径（KeyPath），表示要更新的对象的属性。它必须是一个可写的属性。在键路径中，你指定了要更新的属性在对象中的位置。

- `object`：这是一个表示要更新属性的对象的引用。通常，它是你希望属性值与发布者的输出值保持同步的对象。

- 返回值：`assign(to:on:)` 方法返回一个 `AnyCancellable`，这是一个可用于取消订阅的对象。你可以选择保留此对象，以便稍后手动取消订阅。

以下是一个示例，演示如何使用 `assign(to:on:)` 方法将 Combine 发布者的输出值分配给对象的属性：

```swift
import Combine

class ExampleObject {
    @Published var value: String = ""
}

let object = ExampleObject()

let publisher = Just("Hello, World!")

// 使用assign(to:on:)方法将发布者的输出值分配给对象的属性
let cancellable = publisher
    .assign(to: \.value, on: object)

print(object.value) // 输出: Hello, World!
```

在上面的示例中，我们创建了一个名为 `ExampleObject` 的类，该类具有一个 `@Published` 属性 `value`，表示一个可被订阅的属性。然后，我们使用 `assign(to:on:)` 方法将 `Just` 发布者的输出值 "Hello, World!" 分配给 `ExampleObject` 实例的 `value` 属性，从而将属性值更新为 "Hello, World!"。

这种方法非常有用，因为它允许你轻松地将 Combine 数据流中的值与对象属性同步，无需手动更新属性或编写回调函数。





在 Combine 框架中，`assign(to:on:)` 是一个发布者（Publisher）的扩展方法，它允许你将发布者的输出值（Outputs）自动分配给一个可写的属性（WritableKeyPath）上，这个属性通常位于某个对象（Root）上。当发布者发出新值时，这个新值会自动被分配给属性。

方法签名如下：

```swift
public func assign<Root>(to keyPath: ReferenceWritableKeyPath<Root, Self.Output>, on object: Root) -> AnyCancellable
```

这个方法的参数解释如下：

- `keyPath`：一个 `ReferenceWritableKeyPath`，表示要分配发布者的输出值的属性。这个属性必须是可写的，以便接收新值。

- `object`：一个表示包含要分配属性的对象（Root）的实例。

这个方法的主要作用是将 Combine 的发布者与对象属性绑定，以便在发布者发出新值时，自动将新值分配给属性。这对于将数据流与用户界面元素（例如 `@State`、`@Published` 等）绑定非常有用，以实现数据驱动的用户界面更新。

以下是一个示例，演示如何使用 `assign(to:on:)` 方法将发布者的输出值分配给对象的属性：

```swift
import SwiftUI
import Combine

class ViewModel: ObservableObject {
    @Published var message: String = ""
    
    private var cancellables: Set<AnyCancellable> = []

    init() {
        // 创建一个发布者，每秒发送一个消息
        let publisher = Timer.publish(every: 1, on: .main, in: .default)
            .autoconnect()
            .map { _ in "Message at \(Date())" }
            .assign(to: \.message, on: self) // 将发布者的输出值分配给 message 属性
    }
}

struct ContentView: View {
    @ObservedObject var viewModel = ViewModel()

    var body: some View {
        Text(viewModel.message)
    }
}

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

在上面的示例中，我们创建了一个名为 `ViewModel` 的 ObservableObject 类，它包含一个 `@Published` 属性 `message`，该属性表示要在用户界面上显示的消息。我们使用 `assign(to:on:)` 方法将发布者的输出值分配给 `message` 属性，以便在定时器发出的消息时，自动更新用户界面。

这个方法使得在 SwiftUI 中实现响应式的用户界面非常方便，因为它自动将数据流与界面元素绑定，使界面能够根据数据的变化进行更新。




### 17.4 ObservableObject的@Published属性是 Publisher

`ObservableObject` 中的 `@Published` 属性本质上是 Combine 框架中的发布者（Publisher）。`@Published` 属性用于将对象的属性转化为发布者，以便能够监视和订阅属性的变化。当属性值发生变化时，发布者将自动发出新的值，从而使订阅者能够响应属性的变化。

在 SwiftUI 中，`@Published` 属性通常用于将视图模型（ViewModel）中的属性与用户界面元素绑定。当属性的值发生变化时，用户界面将自动更新以反映新的值。

以下是一个示例，演示如何在 SwiftUI 中使用 `@Published` 属性：

```swift
import SwiftUI
import Combine

class ViewModel: ObservableObject {
    @Published var message: String = "Initial message"
    
    func updateMessage() {
        message = "Updated message at \(Date())"
    }
}

struct ContentView: View {
    @ObservedObject var viewModel = ViewModel()

    var body: some View {
        VStack {
            Text(viewModel.message)
            Button("Update Message") {
                viewModel.updateMessage()
            }
        }
    }
}

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

在这个示例中，`@Published` 属性 `message` 是一个发布者，它与 `ContentView` 中的文本视图绑定。当用户点击按钮以更新消息时，`updateMessage()` 方法将更改 `message` 属性的值，而发布者将自动通知视图更新以反映新的消息。

这种方式使得在 SwiftUI 中实现响应式的用户界面非常方便，因为它允许你使用 Combine 的功能来管理数据流，从而实现用户界面与数据的双向绑定。



### 17.5  Publisher 的扩展`public func assign(to published: inout Published<Self Output>.Publisher).`

`assign(to:)` 是 Combine 中 `Publisher` 的扩展方法之一，用于将发布者的输出值分配给 `@Published` 属性的发布者，实现数据流的绑定。这对于在 SwiftUI 中实现响应式的用户界面非常有用。

方法签名如下：

```swift
public func assign(to published: inout Published<Self.Output>.Publisher) -> AnyCancellable
```

让我们解释一下这个方法的参数：

- `published`: 这是一个 `Published<Self.Output>.Publisher` 类型的输入参数，通常表示一个 `@Published` 属性的发布者。这个参数是一个 `inout` 参数，表示你要将发布者的输出值分配给这个属性的发布者。

使用 `assign(to:)` 方法时，你只需传递一个 `@Published` 属性的发布者，方法将自动将发布者的输出值分配给该属性的发布者。这意味着当发布者发出新值时，它将自动更新与该属性相关联的用户界面。

以下是一个示例，演示如何使用 `assign(to:)` 方法将发布者的输出值分配给 `@Published` 属性的发布者：

```swift
import SwiftUI
import Combine

class ViewModel: ObservableObject {
    @Published var message: String = "Initial message"
    
    private var cancellables: Set<AnyCancellable> = []

    init() {
        // 创建一个发布者，每秒发送一个消息
        let publisher = Timer.publish(every: 1, on: .main, in: .default)
            .autoconnect()
            .map { _ in "Message at \(Date())" }
        
        // 使用 assign(to:) 方法将发布者的输出值分配给 @Published 属性的发布者
        publisher.assign(to: &$message)
    }
}

struct ContentView: View {
    @ObservedObject var viewModel = ViewModel()

    var body: some View {
        Text(viewModel.message)
    }
}

@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```

在这个示例中，我们创建了一个名为 `ViewModel` 的 `ObservableObject` 类，它包含一个 `@Published` 属性 `message`，表示要在用户界面上显示的消息。我们使用 `assign(to:)` 方法将发布者的输出值分配给 `message` 属性的发布者，以便在定时器发出的消息时，自动更新用户界面。

这种方式使得在 SwiftUI 中实现响应式的用户界面非常方便，因为它允许你使用 Combine 的功能来管理数据流，实现用户界面与数据的双向绑定。



### 17.6 熟悉Key-Valve 监视的接口后，可以很方便地应用的项目中

了解和熟练使用 Combine 中的 Key-Value Observing (KVO) 监视接口是在 SwiftUI 和 Combine 框架中进行数据绑定和响应式编程的关键部分。通过监视对象的属性变化，你可以轻松地将数据流与用户界面元素绑定，实现响应式的用户界面更新。以下是一些常见的情景和项目中的应用：

1. **数据绑定和用户界面更新**：在 SwiftUI 中，你可以使用 `@Published` 属性和 Combine 的 `assign(to:)` 方法来将数据与用户界面元素绑定。当数据发生变化时，用户界面将自动更新，无需手动编写界面更新代码。

2. **网络请求和数据加载**：使用 Combine 发布者来执行网络请求，然后使用监视接口来更新用户界面以显示加载的数据。这对于展示从网络获取的数据非常有用。

3. **表单验证和实时反馈**：你可以监视表单中的输入字段，以验证输入的数据并实时提供反馈。例如，当密码强度发生变化时，可以自动更新强度指示器。

4. **用户界面状态管理**：通过监视状态变量，可以轻松管理用户界面的状态。例如，在登录过程中，可以监视登录状态，以在用户登录成功或失败时更新界面。

5. **用户偏好设置和本地存储**：将用户偏好设置与用户界面元素绑定，以实现实时的用户配置更改，同时使用监视接口来更新存储的设置。

6. **实时数据更新**：对于需要实时数据更新的应用程序，可以使用监视接口来监视数据源的变化，并在数据发生变化时自动更新用户界面。

7. **错误处理和通知**：监视错误变量，以在应用程序中出现错误时提供适当的通知或反馈。

8. **事件处理和响应**：通过监视事件变量，可以自动触发特定操作或处理事件。例如，在游戏应用中，监视分数变化以更新用户界面。

总之，Combine 中的监视接口为响应式编程提供了强大的工具，使开发人员能够更轻松地管理数据流和用户界面的交互。它可以用于各种应用程序场景，从简单的用户界面更新到复杂的数据流处理和事件管理。



## 18. 并发编程概念回顾

理解iOS中多线程概念和用语。
理解DispatchQueue优先级。
理解semaphore的工作流程和使用示例。
理解同步和异步 在DispatchQueve 的执行。

### 18.1 iOS中多线程概念和用语。

多线程是 iOS 开发中的重要概念，用于同时执行多个任务，以提高应用程序的性能和响应性。以下是一些与多线程相关的重要概念和用语：

1. **线程（Thread）**：线程是操作系统中的最小执行单元，它可以独立运行代码。在 iOS 中，主线程（Main Thread）是应用程序的主要线程，用于处理用户界面操作。应用程序还可以创建其他线程来执行后台任务。

2. **并发（Concurrency）**：并发是指在同一时间段内执行多个任务的能力。iOS 应用程序通常使用多线程来实现并发，以确保在处理复杂任务时不会阻塞用户界面。

3. **多线程编程（Multithreading）**：多线程编程是一种编程模式，用于同时执行多个线程以提高性能。在 iOS 开发中，多线程编程可以通过 GCD（Grand Central Dispatch）和操作队列来实现。

4. **GCD（Grand Central Dispatch）**：GCD 是苹果提供的多线程编程框架，用于简化多线程编程。它提供了一个并发队列（Concurrent Queue）的概念，允许开发人员轻松地执行任务并管理多线程。

5. **队列（Queue）**：队列是 GCD 中的基本概念，用于管理任务的执行。队列分为串行队列（Serial Queue）和并发队列（Concurrent Queue）。串行队列逐个执行任务，而并发队列可以同时执行多个任务。

6. **任务（Task）**：任务是要在队列上执行的工作单元。任务可以是同步任务（Synchronous Task）或异步任务（Asynchronous Task）。异步任务不会阻塞当前线程，而同步任务会等待任务完成后才继续执行。

7. **主队列（Main Queue）**：主队列是一个串行队列，用于执行与用户界面相关的任务。它通常用于更新用户界面元素，因为只有主线程可以更新用户界面。

8. **全局队列（Global Queue）**：全局队列是一个并发队列，用于执行后台任务。它根据优先级分为多个队列，包括高、中、低和后台四种优先级。

9. **线程安全（Thread Safety）**：线程安全是指在多线程环境中，数据和资源可以被多个线程同时访问而不会导致不一致或异常。线程安全的编程是确保多线程应用程序的数据完整性的关键。

10. **死锁（Deadlock）**：死锁是一种多线程编程错误，其中多个线程相互等待对方释放资源，从而导致程序停滞。死锁是应该避免的情况。

11. **并发队列组（Dispatch Group）**：并发队列组是一种用于等待多个任务完成的机制。它允许你等待一组任务全部完成后才继续执行其他操作。

12. **同步（Synchronization）**：同步是一种控制多个线程访问共享资源的机制，以确保数据的一致性。同步可以通过锁（Locks）和信号量（Semaphores）等方式实现。

13. **原子操作（Atomic Operations）**：原子操作是不可分割的操作，它不会被其他线程中断。原子操作通常用于多线程环境下的数据访问，以确保数据的一致性。

这些概念和用语对于理解和处理多线程编程在 iOS 开发中非常重要。多线程编程可以提高应用程序的性能和响应性，但也需要小心处理，以避免潜在的问题，如竞态条件和死锁。 GCD 是 iOS 开发中的主要多线程编程工具，它提供了简单而强大的方式来管理多线程任务。



### 18.2 队列DispatchQueue优先级。

`DispatchQueue` 优先级是用于管理任务执行顺序的一种机制。iOS 开发中，你可以使用 GCD（Grand Central Dispatch）来创建并管理队列，并为队列设置不同的优先级以控制任务的执行顺序。以下是关于 `DispatchQueue` 优先级的一些重要信息：

1. **优先级级别**：`DispatchQueue` 优先级有四个级别，从高到低分别是：
   - `.userInteractive`：最高优先级，用于执行与用户交互相关的任务，例如 UI 更新和响应用户输入。
   - `.userInitiated`：较高优先级，用于执行用户请求的任务，但不需要立即响应。
   - `.default`：默认优先级，通常用于普通后台任务。
   - `.utility`：低优先级，用于执行长时间运行的任务，不需要立即完成。

2. **全局队列**：`DispatchQueue` 的全局队列包含多个队列，每个队列都有一个特定的优先级。你可以使用 `DispatchQueue.global(qos: .priority)` 来获取全局队列，并传入相应的优先级，以获得不同优先级的队列。

3. **自定义队列**：除了全局队列，你还可以创建自定义队列，并为其指定优先级。自定义队列通常用于组织和执行你的应用程序的特定任务。

4. **优先级影响**：队列的优先级决定了其上任务的执行顺序。具有更高优先级的队列上的任务将在具有较低优先级的队列上的任务之前执行。然而，这并不意味着高优先级任务会立即执行，因为任务的执行还受到系统资源和可用线程的限制。

5. **多线程环境下的注意事项**：设置队列的优先级通常是为了控制任务的执行顺序，但并不是用于调整任务的速度。在多线程环境中，你仍然需要小心处理共享资源的同步和线程安全，以避免竞态条件和数据不一致的问题。

以下是一个示例，演示如何创建一个自定义队列并为其设置不同的优先级：

```swift
import Foundation

// 创建一个自定义队列，优先级为 .userInteractive
let highPriorityQueue = DispatchQueue(label: "com.example.highPriority", qos: .userInteractive)

// 创建一个自定义队列，优先级为 .utility
let lowPriorityQueue = DispatchQueue(label: "com.example.lowPriority", qos: .utility)

// 在高优先级队列上执行任务
highPriorityQueue.async {
    print("High Priority Task 1")
}

// 在低优先级队列上执行任务
lowPriorityQueue.async {
    print("Low Priority Task 1")
}

// 主队列上执行任务
DispatchQueue.main.async {
    print("Main Queue Task")
}

// 在高优先级队列上执行另一个任务
highPriorityQueue.async {
    print("High Priority Task 2")
}
```

在这个示例中，我们创建了两个自定义队列，一个设置为高优先级（.userInteractive），另一个设置为低优先级（.utility）。任务在这些队列上执行的顺序受到队列的优先级影响，高优先级队列上的任务首先执行，然后是低优先级队列上的任务，最后是主队列上的任务。

理解和使用队列的优先级有助于在应用程序中更好地管理任务的执行顺序，从而提高性能和响应性。



### 18.3 信号量semaphore的工作流程和使用示例

信号量（Semaphore）是一种用于控制多线程访问共享资源的同步机制。信号量允许你限制同时访问共享资源的线程数量。在 iOS 开发中，你可以使用信号量来解决一些多线程编程中的同步问题。以下是信号量的工作流程和使用示例：

**工作流程：**

1. 信号量（Semaphore）是一个整数计数器，它具有一个初始值。
2. 当线程要访问共享资源时，它必须尝试获取信号量。
3. 如果信号量的计数器大于零，线程可以获得信号量，计数器减一。
4. 如果信号量的计数器等于零，线程将被阻塞，直到有其他线程释放信号量。
5. 当线程完成对共享资源的访问后，它释放信号量，计数器加一。
6. 其他被阻塞的线程可以继续获取信号量并访问共享资源。

**使用示例：**

以下是一个简单的示例，演示了如何使用信号量来限制同时执行的线程数量，以控制并发访问一个临界区域的情况：

```swift
import Foundation

// 创建一个信号量，初始值为3，表示同时允许3个线程访问临界区域
let semaphore = DispatchSemaphore(value: 3)

// 模拟多个线程访问共享资源的情况
for i in 1...10 {
    DispatchQueue.global().async {
        // 尝试获取信号量，如果计数器大于零，则获取成功
        semaphore.wait()
        
        // 访问共享资源
        print("Thread \(i) is accessing the critical section")
        // 模拟访问共享资源的耗时操作
        sleep(2)
        
        // 释放信号量，表示线程访问结束
        semaphore.signal()
    }
}

// 等待所有线程执行完毕
sleep(10)
```

在这个示例中，我们创建了一个初始值为3的信号量。然后，我们模拟了10个线程尝试访问一个临界区域，但由于信号量的限制，最多只能有3个线程同时访问。

线程在进入临界区域之前使用 `semaphore.wait()` 尝试获取信号量，如果计数器大于零，则获取成功，否则线程将被阻塞。在访问共享资源后，线程使用 `semaphore.signal()` 释放信号量，表示访问结束，这样其他被阻塞的线程可以继续执行。

使用信号量可以有效地控制并发访问共享资源的线程数量，从而避免竞态条件和提高多线程编程的稳定性。



### 18.4 同步和异步 在DispatchQueve 的执行

在 GCD (Grand Central Dispatch) 中，任务可以在队列上以同步（synchronous）或异步（asynchronous）方式执行。这两种执行方式的主要区别在于任务是否会立即返回给调用方以及任务在队列上的执行方式。

**同步执行（Synchronous）**：

1. 同步执行意味着任务将在当前线程上执行，而不会创建新的线程。

2. 调用线程将等待任务完成，只有当任务执行完毕后，控制才会返回给调用方。

3. 同步执行通常用于确保在当前线程中执行某些任务，例如在主线程中执行 UI 更新。

示例：

```swift
let queue = DispatchQueue.global()

queue.sync {
    // 这个任务将同步执行，当前线程会等待任务完成
}
```

**异步执行（Asynchronous）**：

1. 异步执行意味着任务将在后台线程上执行，不会阻塞当前线程。

2. 调用线程不会等待任务完成，而是继续执行后续的代码。

3. 异步执行通常用于在后台线程上执行耗时操作，以避免阻塞主线程，保持应用的响应性。

示例：

```swift
let queue = DispatchQueue.global()

queue.async {
    // 这个任务将异步执行，当前线程不会等待任务完成
}
```

需要注意的是，异步执行在多线程环境中可以提高应用的性能和响应性，但也需要小心处理线程同步和竞争条件的问题。此外，异步任务的执行顺序不能保证与提交的顺序相同，因为多个任务可能会在不同的线程上并行执行。

总结：同步执行会在当前线程上执行任务并阻塞调用线程，而异步执行会在后台线程上执行任务并不阻塞调用线程。选择使用哪种方式取决于你的需求和线程管理策略。




## 19. Share和Multicast Operators

-**目标**：
使用share 或 Multicast 的原因是为了共享资源，减少不必要的资源请求（或使用）；
Connectable是可以更好的控制订阅有效的时间点；
体会Future 和 Share 并用时，订阅处理的时间点；
理解publisher的receive data的次数。
理解share Operator。
理解make Connectable Operator。
理解multicast(subject) operator。
理解share Operator和 Future的使用。

### 19.1 publisher的receive data的次数

在 Combine 中，一个 Publisher（发布者）可以通过多次调用 `sink` 或其他订阅操作符来订阅，从而接收多次数据。每次订阅都会触发数据流的开始，并且数据流中的数据将从头开始发送。这就意味着，如果您多次订阅同一个 Publisher，它将发送相同的数据序列多次。

以下是一个示例，演示了多次订阅同一个 Publisher 时，数据会被发送多次：

```swift
import Combine

let publisher = Just("Hello, Combine")

// 第一次订阅
let cancellable1 = publisher.sink { value in
    print("Subscriber 1 received: \(value)")
}

// 第二次订阅
let cancellable2 = publisher.sink { value in
    print("Subscriber 2 received: \(value)")
}

// 输出:
// Subscriber 1 received: Hello, Combine
// Subscriber 2 received: Hello, Combine
```

在上述示例中，我们首先订阅了 `publisher` 两次，并且两个订阅者都接收到了相同的数据。这是因为每次订阅都会从头开始数据流。

需要注意的是，多次订阅同一个 Publisher 可能会导致相同的数据被处理多次。如果您希望多个订阅者共享相同的数据流，您可以使用 `share` 操作符或 `multicast` 操作符来共享数据流，以确保数据只被处理一次。这有助于避免不必要的重复工作。



### 19.2 share Operator

`share` 操作符是 Combine 中的一个有用操作符，它用于共享订阅者之间的数据，并将一个发布者连接到多个订阅者，以避免多次执行发布者的操作。它通常在需要多次共享相同数据流的情况下非常有用，以减少不必要的重复工作。

以下是 `share` 操作符的基本工作方式和示例：

**工作方式**：
1. 当一个发布者上应用 `share` 操作符时，它创建一个共享订阅者，该共享订阅者会订阅原始发布者。
2. 共享订阅者将数据项缓存，并将其发送给所有订阅它的订阅者。
3. 共享订阅者只与原始发布者建立一次订阅关系，以避免多次触发发布者的操作。

**示例**：
```swift
import Combine

let numbers = [1, 2, 3, 4, 5]

let publisher = numbers.publisher

let sharedPublisher = publisher.share()

let subscriber1 = sharedPublisher.sink { value in
    print("Subscriber 1 received: \(value)")
}

let subscriber2 = sharedPublisher.sink { value in
    print("Subscriber 2 received: \(value)")
}

// 输出：
// Subscriber 1 received: 1
// Subscriber 2 received: 1
// Subscriber 1 received: 2
// Subscriber 2 received: 2
// Subscriber 1 received: 3
// Subscriber 2 received: 3
// Subscriber 1 received: 4
// Subscriber 2 received: 4
// Subscriber 1 received: 5
// Subscriber 2 received: 5
```

在上述示例中，我们创建了一个发布者 `publisher`，然后使用 `share` 操作符创建了 `sharedPublisher`。两个不同的订阅者 `subscriber1` 和 `subscriber2` 订阅了 `sharedPublisher`。当数据项通过 `sharedPublisher` 发出时，它们会同时传递给两个订阅者，而不会触发 `publisher` 的操作多次。

`share` 操作符是确保多个订阅者可以共享相同数据流的有用工具，特别是在处理复杂的数据流时，可以减少性能开销和不必要的计算。



### 19.3 make Connectable Operator

`makeConnectable` 不是 Combine 中的标准操作符，但它可以用于创建可连接的发布者（Connectable Publisher）。一个可连接的发布者是一种特殊类型的发布者，它需要显式调用 `connect()` 方法，以触发数据流的开始。

以下是一个自定义的 `makeConnectable` 操作符的示例，它创建一个可连接的发布者：

```swift
import Combine

extension Publisher {
    func makeConnectable() -> ConnectablePublisher<Self> {
        return self.share().makeConnectable()
    }
}

let numbers = [1, 2, 3, 4, 5]

let publisher = numbers.publisher.makeConnectable()

let subscriber1 = publisher.sink { value in
    print("Subscriber 1 received: \(value)")
}

let subscriber2 = publisher.sink { value in
    print("Subscriber 2 received: \(value)")
}

print("Connected")
publisher.connect() // 手动连接可连接的发布者

// 输出：
// Connected
// Subscriber 1 received: 1
// Subscriber 2 received: 1
// Subscriber 1 received: 2
// Subscriber 2 received: 2
// Subscriber 1 received: 3
// Subscriber 2 received: 3
// Subscriber 1 received: 4
// Subscriber 2 received: 4
// Subscriber 1 received: 5
// Subscriber 2 received: 5
```

在上述示例中，我们扩展了 `Publisher`，添加了一个自定义的 `makeConnectable` 操作符。它使用 `share` 操作符来创建一个可共享的发布者，然后使用 `makeConnectable()` 方法将其转换为可连接的发布者。两个不同的订阅者 `subscriber1` 和 `subscriber2` 订阅了可连接的发布者。最后，我们手动调用 `connect()` 方法来启动数据流。

这个示例展示了如何创建自定义的可连接发布者，以及如何手动触发数据流的开始。这在某些需要精确控制数据流启动时机的情况下非常有用。但需要注意，通常情况下，`share` 操作符已经提供了一个方便的方式来创建可连接的发布者，而不需要手动创建。




### 19.4 multicast(subject) operator

`multicast` 操作符是 Combine 中的一个有用操作符，它允许你将一个发布者（Publisher）共享给多个订阅者（Subscriber），并使用自定义的主题（Subject）来控制数据流。这使你能够更灵活地管理数据的传递和订阅者之间的通信。

以下是 `multicast` 操作符的基本工作方式和示例：

**工作方式**：
1. `multicast` 操作符需要一个主题（Subject）作为参数。主题是一种既是发布者又是订阅者的类型，用于控制数据流。
2. 当你应用 `multicast` 操作符时，它会创建一个主题，并将原始发布者连接到这个主题上。
3. 然后，你可以将多个订阅者订阅这个主题，以接收来自主题的数据。
4. 主题负责将来自原始发布者的数据转发给所有订阅它的订阅者。

**示例**：
```swift
import Combine

let numbers = [1, 2, 3, 4, 5]

let publisher = numbers.publisher

let subject = PassthroughSubject<Int, Never>() // 创建一个 PassthroughSubject 作为主题

let multicastPublisher = publisher.multicast(subject: subject)

let subscriber1 = multicastPublisher.sink { value in
    print("Subscriber 1 received: \(value)")
}

let subscriber2 = multicastPublisher.sink { value in
    print("Subscriber 2 received: \(value)")
}

multicastPublisher.connect() // 手动连接发布者和主题

// 输出：
// Subscriber 1 received: 1
// Subscriber 2 received: 1
// Subscriber 1 received: 2
// Subscriber 2 received: 2
// Subscriber 1 received: 3
// Subscriber 2 received: 3
// Subscriber 1 received: 4
// Subscriber 2 received: 4
// Subscriber 1 received: 5
// Subscriber 2 received: 5
```

在上述示例中，我们使用 `multicast` 操作符将原始发布者 `publisher` 连接到一个主题 `subject` 上。然后，我们创建两个订阅者 `subscriber1` 和 `subscriber2`，它们订阅了 `multicastPublisher`，从主题接收数据。最后，我们手动调用 `connect()` 方法来启动数据流。

`multicast` 操作符允许你自定义主题，这对于实现特定的数据流控制逻辑非常有用。你可以选择不同类型的主题（例如 `PassthroughSubject`、`CurrentValueSubject` 等），根据需要控制数据的传递方式。

这个操作符非常适合在需要在多个订阅者之间共享数据流时使用，以确保数据只被生成一次，而且多个订阅者可以独立处理这些数据。



19.5 share Operator和 Future的使用
`share` 操作符和 `Future` 类型都是 Combine 框架中常用的工具，用于处理异步数据流和多个订阅者之间的数据共享。以下是它们的使用示例：

**使用 `share` 操作符**：

`share` 操作符用于将一个发布者（Publisher）转换为可连接的发布者，从而允许多个订阅者共享同一个数据流。这对于减少多次触发发布者操作、提高性能和减少资源消耗非常有用。

```swift
import Combine

let numbers = [1, 2, 3, 4, 5]

let publisher = numbers.publisher

let sharedPublisher = publisher.share()

let subscriber1 = sharedPublisher.sink { value in
    print("Subscriber 1 received: \(value)")
}

let subscriber2 = sharedPublisher.sink { value in
    print("Subscriber 2 received: \(value)")
}

// 输出：
// Subscriber 1 received: 1
// Subscriber 2 received: 1
// Subscriber 1 received: 2
// Subscriber 2 received: 2
// Subscriber 1 received: 3
// Subscriber 2 received: 3
// Subscriber 1 received: 4
// Subscriber 2 received: 4
// Subscriber 1 received: 5
// Subscriber 2 received: 5
```

在上述示例中，`share` 操作符创建了一个可连接的发布者，从中订阅者 `subscriber1` 和 `subscriber2` 都可以接收相同的数据流。

**使用 `Future` 类型**：

`Future` 是 Combine 中的一种发布者，它用于表示将来会生成一个值的异步操作。你可以使用 `Future` 来包装一个异步任务，然后在任务完成时将值发送给订阅者。

```swift
import Combine

func asyncOperation() -> Future<String, Error> {
    return Future { promise in
        DispatchQueue.global().async {
            // 模拟异步操作
            sleep(2)
            promise(.success("Operation completed"))
        }
    }
}

let future = asyncOperation()

let subscriber = future.sink(
    receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Future completed")
        case .failure(let error):
            print("Future failed with error: \(error)")
        }
    },
    receiveValue: { value in
        print("Future received value: \(value)")
    }
)

// 输出：
// Future received value: Operation completed
// Future completed
```

在上述示例中，`asyncOperation` 函数返回一个 `Future`，表示一个异步操作。当操作完成后，`Future` 发送成功的值给订阅者，并在完成时通知订阅者。这可用于处理各种异步任务，例如网络请求、文件读写等。

`share` 操作符和 `Future` 类型在 Combine 中都具有重要的作用，可以在异步数据流和多个订阅者之间提供方便的数据共享和处理方式。



## 20. Scheduler
**目标：**
充分理解Combine中使用sUbscribe (on)和receive (on)切换
Scheduler对于不同种类的task的执行安排，对资源使用有着重要意义，
不仅仅是为了提高用户体验。

理解Scheduler的概念。
了解各种Scheduler。
理解Combine使用切换上游和下游的执行上下文。
理解subscribe(on)和receive(on)的接口定义。

### 20.1 Scheduler的概念

在 Combine 和 Swift 中，`Scheduler` 是一种抽象的机制，用于管理和调度异步任务的执行。它允许你指定任务何时执行，以及在哪个线程或队列上执行。`Scheduler` 是处理时间、定时器、延迟任务和异步操作的核心组件之一。

下面是一些与 `Scheduler` 相关的重要概念：

1. **`DispatchQueue` 和 `OperationQueue`**：这是 iOS 和 macOS 中用于执行任务的常见调度器。它们允许你将任务调度到不同的队列中，例如主队列（`main`）或后台队列，以实现多线程操作。

2. **`Runloop`**：在 macOS 和 iOS 中，`Runloop` 是一个事件处理循环，用于管理用户事件、计时器和输入事件。它允许你安排任务在特定的 runloop 模式中执行。

3. **`OperationQueue`**：`OperationQueue` 是 GCD（Grand Central Dispatch）的高级封装，它提供了更多控制和管理多线程任务的能力。

4. **`AnyScheduler`**：Combine 框架中引入了 `AnyScheduler`，它是一个协议，用于抽象各种调度器。这允许你更容易地进行单元测试，因为你可以使用虚拟调度器来模拟时间的流逝。

5. **`Publishers.Timer`**：Combine 中的 `Timer` 发布者使用 `Scheduler` 来定时生成数据流。

6. **定时任务**：`Scheduler` 允许你安排任务在未来的某个时间点执行，或者以间隔定期执行。这对于执行后台任务、轮询服务器或管理计时器非常有用。

总之，`Scheduler` 是一个关键的概念，用于管理异步任务的执行，它允许你精确地控制何时和在哪里执行任务。不同的平台和框架可能提供不同类型的调度器，用于满足特定的需求，但它们都遵循相似的原则，允许你管理时间和任务的流程。



### 20.2 各种Scheduler

在 Combine 和 Swift 中，有各种不同类型的调度器（Schedulers），用于管理和调度异步任务的执行。这些调度器允许你指定任务何时执行以及在哪个线程或队列上执行。以下是一些常见的调度器：

1. **DispatchQueue**：`DispatchQueue` 是 Swift 中的调度器，用于执行任务。它提供了多种队列，包括主队列（`main`）和后台队列（`global`），可以用于并行和串行任务。例如，你可以使用 `DispatchQueue.main` 来在主线程上执行任务，或使用 `DispatchQueue.global(qos: .background)` 来在后台队列上执行任务。

2. **OperationQueue**：`OperationQueue` 是 GCD（Grand Central Dispatch）的高级封装，允许你管理和控制并发任务。你可以创建自己的 `OperationQueue` 实例，并将任务添加到队列中以进行并行处理。

3. **RunLoop**：`RunLoop` 是 macOS 和 iOS 中的事件处理循环。你可以使用 `RunLoop` 调度器来将任务安排在特定的 runloop 模式中执行，通常用于处理输入事件、计时器和网络请求。

4. **ImmediateScheduler**：`ImmediateScheduler` 是 Combine 提供的一种调度器，用于立即执行任务。它通常用于单元测试，以模拟立即执行任务的情况。

5. **AnyScheduler**：`AnyScheduler` 是 Combine 中的协议，允许你封装任何实际的调度器，并使用它来抽象调度器的行为。这对于单元测试和依赖注入非常有用。

6. **Publishers.MainQueue**：`Publishers.MainQueue` 是 Combine 中的一个调度器，用于在主队列上执行任务。它通常用于确保 UI 更新在主线程上执行。

7. **Publishers.Timer**：`Publishers.Timer` 是 Combine 提供的一个调度器，用于定时执行任务。你可以使用它来创建定时器，以在未来的某个时间点执行任务。

这些调度器可以根据不同的需求来选择，以确保任务在适当的时间和线程上执行。它们是异步编程的重要工具，用于管理时间、并发和任务的调度。




### 20.3 Combine使用切换上游和下游的执行上下文

在 Combine 中，你可以使用操作符来切换上游和下游的执行上下文，以确保任务在不同的线程或队列上执行。这对于控制数据流的执行环境非常有用，以避免阻塞主线程或在后台线程上执行长时间运行的任务。以下是一些常用的操作符和方法来实现上下文切换：

1. **receive(on:) 操作符**：`receive(on:` 操作符允许你切换下游（订阅者）的执行上下文。你可以传递一个 `Scheduler`，以指定在哪个线程或队列上接收数据。例如，你可以将数据切换到主队列以更新用户界面：

```swift
let publisher = fetchDataPublisher() // 假设这是一个异步数据获取的发布者

let mainQueueScheduler = DispatchQueue.main

let subscriber = publisher
    .receive(on: mainQueueScheduler) // 切换到主队列
    .sink { data in
        // 在主队列上更新 UI
        updateUI(data)
    }
```

2. **subscribe(on:) 操作符**：`subscribe(on:` 操作符用于切换上游的执行上下文。它可以确保订阅者之前的操作在指定的 `Scheduler` 上执行。这对于将整个数据流移至后台线程以执行耗时任务很有帮助。

```swift
let backgroundQueueScheduler = DispatchQueue.global(qos: .background)

let subscriber = publisher
    .subscribe(on: backgroundQueueScheduler) // 切换到后台队列
    .sink { data in
        // 在后台队列上执行数据处理
        process(data)
    }
```

3. **map 操作符**：`map` 操作符也可以用于切换上下游的执行上下文。在 `map` 操作符中，你可以使用 `receive(on:)` 切换下游的上下文。

```swift
let publisher = fetchDataPublisher()

let mainQueueScheduler = DispatchQueue.main

let subscriber = publisher
    .map { data in
        // 在上游执行映射操作
        return process(data)
    }
    .receive(on: mainQueueScheduler) // 切换到主队列
    .sink { processedData in
        // 在主队列上更新 UI
        updateUI(processedData)
    }
```

这些操作符和方法允许你以灵活的方式控制数据流的执行上下文，确保任务在适当的线程或队列上执行，以提高性能和用户体验。这在异步编程中非常有用，特别是在处理网络请求、文件操作和其他异步任务时。



### 20.4 subscribe(on)和receive(on)的接口定义

在 Combine 中，`subscribe(on:)` 和 `receive(on:)` 操作符用于切换执行上下文，分别用于上游和下游的切换。它们的接口定义如下：

**`subscribe(on:)` 操作符**：

`subscribe(on:)` 操作符用于切换上游的执行上下文，以确保订阅之前的操作在指定的 `Scheduler` 上执行。

```swift
func subscribe<S>(on scheduler: S, options: S.SchedulerOptions? = nil, _ strategy: Combine.Subscribers.Demand.Strategy) -> Publishers.SubscribeOn<Self, S> where S : Scheduler
```

- `scheduler`: 一个遵循 `Scheduler` 协议的对象，用于指定上游任务的执行上下文。
- `options`（可选）：用于配置调度器的选项，例如 `S.SchedulerOptions`。
- `strategy`: 订阅者的需求策略，通常使用默认值即可。

**`receive(on:)` 操作符**：

`receive(on:)` 操作符用于切换下游的执行上下文，以确保数据在指定的 `Scheduler` 上发送给订阅者。

```swift
func receive<S>(on scheduler: S, options: S.SchedulerOptions? = nil) -> Publishers.ReceiveOn<Self, S> where S : Scheduler
```

- `scheduler`: 一个遵循 `Scheduler` 协议的对象，用于指定下游任务的执行上下文。
- `options`（可选）：用于配置调度器的选项，例如 `S.SchedulerOptions`。

这两个操作符都返回新的发布者类型，其中任务的执行上下文已经切换到指定的调度器。这使得你可以根据需求灵活地控制任务的执行位置，以确保合适的性能和线程安全。




## 21 自定义订阅者Subscribers和Subscribers.Demand

**目标：**通过本节，学习订阅者Subscriber自定义，提高接受发布者Publisher数据的能力。


认识为什么需要自定义订阅者（Subscriber）。
重新学习Subscriber 协议。
学习Subscribers.Demand的意义 ，动态控制发布数据次数。
理解Subscriber协议和订阅机制，自定义Subscriber.
使用结构体struct或类Cilass实现 Subscriber协议的不同。


### 21.1 认识为什么需要自定义订阅者（Subscriber）

自定义订阅者（Subscriber）是在 Combine 框架中非常有用的能力，因为它允许你根据特定的需求来处理接收到的数据流。以下是一些常见的原因为什么你可能需要自定义订阅者：

1. **特定处理逻辑**：内置的 Combine 操作符和订阅者通常可以满足常见的需求，但有时你可能需要执行特定的数据处理逻辑，例如对接收到的数据进行复杂的计算、筛选、过滤等。

2. **自定义错误处理**：自定义订阅者允许你在出现错误时执行自定义的错误处理逻辑，例如记录错误、重试操作、或向用户显示错误消息。

3. **状态管理**：在某些情况下，你可能需要在处理数据流时维护特定的状态信息。自定义订阅者可以帮助你实现这种状态管理。

4. **调试和日志记录**：自定义订阅者可用于添加调试和日志记录，以便更好地了解数据流的行为和流程。

5. **异步操作**：在某些情况下，你可能需要执行异步操作，例如网络请求或文件操作，然后将结果发送给下游。自定义订阅者可以帮助你处理这些异步操作。

6. **测试**：自定义订阅者在单元测试中非常有用，因为你可以创建虚拟的订阅者来模拟数据流的行为，以验证你的代码是否正确。

7. **数据流分发**：自定义订阅者可以用于将数据流分发给多个不同的下游订阅者，以满足不同的需求。

8. **性能优化**：在某些情况下，你可能需要进行性能优化，例如减少内存使用或处理大量数据。自定义订阅者可以让你实施更精细的控制。

总之，自定义订阅者是 Combine 框架的强大功能，它为你提供了灵活性，以根据具体需求来处理数据流。通过自定义订阅者，你可以更好地控制数据流的行为，并满足各种复杂的需求。



### 21.2 复习Subscriber 协议

Combine 框架中的 `Subscriber` 协议是用于自定义订阅者的核心协议。自定义订阅者允许你对接收到的数据流执行特定的操作、处理错误，以及维护状态信息。以下是 `Subscriber` 协议的重要方法和属性：

```swift
protocol Subscriber: Cancellable {
    associatedtype Input
    associatedtype Failure: Error

    func receive(subscription: Subscription)
    func receive(_ input: Input) -> Subscribers.Demand
    func receive(completion: Subscribers.Completion<Failure>)
}
```

- `associatedtype Input`：这是接收的数据类型，也就是数据流中元素的类型。

- `associatedtype Failure`：这是可能发生的错误类型，遵循 `Error` 协议。

- `receive(subscription:)`：当订阅建立时，Combine 框架会调用此方法，将订阅关联的 `Subscription` 传递给订阅者。订阅者可以使用此订阅对象来请求数据和取消订阅。

- `receive(_:)`：当订阅者接收到新的数据元素时，Combine 框架会调用此方法，将数据元素传递给订阅者。订阅者必须返回一个 `Subscribers.Demand` 值，以指示其对更多数据的需求。

- `receive(completion:)`：当数据流完成时，无论是正常完成还是发生错误，Combine 框架会调用此方法，将 `Subscribers.Completion` 传递给订阅者。这个枚举包含 `.finished`（成功完成）和 `.failure(error)`（发生错误）两种情况。

自定义订阅者需要实现这些方法，以定义其行为，包括如何处理接收到的数据元素、订阅建立和数据流完成时的处理。通过实现 `Subscriber` 协议，你可以完全控制数据流的处理过程，以满足你的特定需求。

需要注意的是，通常情况下，开发者更多地使用 `sink` 方法或其他内置的订阅方式，而不是直接实现 `Subscriber` 协议。这是因为 Combine 提供了高级的抽象操作符和订阅方式，可以更方便地处理数据流，同时减少了大部分手动实现 `Subscriber` 协议的需求。



21.3 Subscribers.Demand的意义 ，动态控制发布数据次数

`Subscribers.Demand` 是 Combine 框架中一个重要的类型，用于动态控制发布者（Publisher）发送数据的次数。它表示订阅者（Subscriber）请求从发布者接收数据的需求量。这个需求量可以随时间变化，允许订阅者根据其处理能力来控制数据的接收速度。

`Subscribers.Demand` 是一个值语义的类型，它可以是以下三种情况之一：

1. **无需求**：表示订阅者暂时不需要接收更多的数据，通常用 `.none` 表示。

2. **需要固定数量的数据**：表示订阅者需要接收指定数量的数据元素。例如，`.max(5)` 表示订阅者请求接收 5 个数据元素。

3. **需要不限数量的数据**：表示订阅者需要接收尽可能多的数据，直到数据流完成。通常用 `.unlimited` 表示。

`Subscribers.Demand` 的重要性在于它允许订阅者和发布者之间进行协商，以避免数据流的阻塞或过载。发布者会根据订阅者的需求发送数据，直到需求为零，然后等待订阅者请求更多数据。

这种方式允许在异步流中进行动态流量控制，确保数据以适当的速度传递，从而提高性能和资源利用率。例如，如果订阅者处理速度较慢，它可以向发布者发送 `.max(n)` 需求，以控制接收的数据数量，避免内存占用过大。如果订阅者能够更快地处理数据，它可以逐渐增加需求以接收更多数据。

综上所述，`Subscribers.Demand` 允许发布者和订阅者协同工作，以实现数据流的有效流动，确保数据不被浪费或阻塞。这是 Combine 框架中非常重要的概念，用于构建响应式和异步应用程序。



### 21.4 Subscriber协议和订阅机制，自定义Subscriber

Combine 中的 `Subscriber` 协议是用于自定义订阅者的核心协议。自定义订阅者允许你以你自己的方式处理从发布者发出的数据流。以下是关于 `Subscriber` 协议和订阅机制的重要信息：

1. **Subscriber 协议**：

   `Subscriber` 协议的定义如下：

   ```swift
   protocol Subscriber: Cancellable {
       associatedtype Input
       associatedtype Failure: Error

       func receive(subscription: Subscription)
       func receive(_ input: Input) -> Subscribers.Demand
       func receive(completion: Subscribers.Completion<Failure>)
   }
   ```

   - `associatedtype Input`：表示接收到的数据类型。
   - `associatedtype Failure`：表示可能的错误类型。

   `Subscriber` 协议定义了以下几个方法：
   
   - `receive(subscription:)`：在订阅建立时调用，将订阅对象传递给订阅者，用于管理订阅。
   - `receive(_:)`：在订阅者接收到新的数据元素时调用，将数据元素传递给订阅者，并返回 `Subscribers.Demand`，表示对更多数据的需求。
   - `receive(completion:)`：在数据流完成时调用，无论是正常完成还是发生错误。

2. **订阅机制**：

   订阅机制是 Combine 中的核心概念，它包括以下步骤：

   - 创建一个发布者（Publisher）。
   - 创建一个自定义订阅者，实现 `Subscriber` 协议中的方法。
   - 使用 `subscribe` 方法将订阅者订阅到发布者上。
   - 发布者开始发送数据流，并调用订阅者的方法。

   通过订阅机制，订阅者可以接收和处理来自发布者的数据，以及处理数据流完成的情况。订阅者可以根据自身逻辑来处理数据、进行状态管理、处理错误等。

3. **自定义 Subscriber**：

   自定义订阅者非常有用，因为它们允许你按照自己的需求处理数据流。你可以创建遵循 `Subscriber` 协议的自定义类型，并实现协议中的方法。例如，你可以实现一个自定义订阅者，用于将数据存储到数据库中，或者实现数据流的特定逻辑。

   下面是一个自定义订阅者的示例：

   ```swift
   class MySubscriber: Subscriber {
       typealias Input = String
       typealias Failure = MyError // 自定义错误类型

       private var subscription: Subscription?

       func receive(subscription: Subscription) {
           self.subscription = subscription
           subscription.request(.unlimited) // 请求接收尽可能多的数据
       }

       func receive(_ input: String) -> Subscribers.Demand {
           // 处理接收到的数据
           print("Received data: \(input)")
           return .none // 无需额外数据
       }

       func receive(completion: Subscribers.Completion<MyError>) {
           // 处理数据流完成，包括正常完成和错误
           switch completion {
           case .finished:
               print("Data stream completed successfully.")
           case .failure(let error):
               print("Data stream failed with error: \(error)")
           }
       }

       func cancel() {
           subscription?.cancel()
           subscription = nil
       }
   }
   ```

   自定义订阅者可以根据你的具体需求实现不同的逻辑，以处理接收到的数据和错误。

通过自定义 `Subscriber`，你可以更灵活地控制数据流的行为，并适应各种复杂的需求。这对于构建响应式和异步应用程序非常有帮助。



### 21.5 使用结构体struct或类Cilass实现 Subscriber协议的不同

使用结构体（`struct`）或类（`class`）来实现 `Subscriber` 协议的不同主要涉及值类型与引用类型的特性。以下是它们的主要区别：

**使用结构体实现 Subscriber 协议：**

1. **值类型**：结构体是值类型，因此在不同的地方拥有独立的拷贝。这意味着每个结构体实例在内存中都是唯一的，修改一个结构体实例不会影响其他实例。

2. **不可变性**：结构体是通常不可变的，这意味着一旦创建，它们的属性不能被修改。这对于表示不变的数据很有用。

3. **线程安全**：由于结构体是不可变的，它们通常更容易实现线程安全。多个线程可以同时访问不可变的结构体实例而不引起竞争条件。

4. **生命周期管理**：结构体没有生命周期管理的问题，因为它们不涉及引用计数。它们在作用域结束时自动销毁。

**使用类实现 Subscriber 协议：**

1. **引用类型**：类是引用类型，多个引用可以指向同一个实例，修改一个实例会影响所有引用。这意味着类可以共享状态和数据。

2. **可变性**：类可以是可变的，其属性可以在运行时更改。这对于需要动态变化的数据结构很有用。

3. **继承**：类支持继承，你可以创建子类来扩展或修改现有的订阅者逻辑。

4. **生命周期管理**：类需要显式管理内存和生命周期，因为它们涉及引用计数。这可能需要处理循环引用和内存泄漏。

选择结构体或类来实现 `Subscriber` 协议取决于你的具体需求和应用场景。如果你只需要执行简单的数据处理逻辑，结构体可能足够。如果你需要共享状态、进行复杂的操作或需要动态变化的逻辑，类可能更适合。记住，结构体和类在适当的情况下都可以用于创建自定义的订阅者，以满足不同的订阅需求。




以下是使用结构体和类分别实现 `Subscriber` 协议的代码示例：

**使用结构体实现 Subscriber 协议**：

```swift
import Combine

struct MyStructSubscriber: Subscriber {
    typealias Input = String
    typealias Failure = Never

    func receive(subscription: Subscription) {
        subscription.request(.unlimited)
    }

    func receive(_ input: String) -> Subscribers.Demand {
        print("Received data in struct subscriber: \(input)")
        return .none
    }

    func receive(completion: Subscribers.Completion<Never>) {
        print("Data stream completed in struct subscriber.")
    }
}

let publisher = Just("Hello, Combine!")
let subscriber = MyStructSubscriber()

publisher.subscribe(subscriber)
```

**使用类实现 Subscriber 协议**：

```swift
import Combine

class MyClassSubscriber: Subscriber {
    typealias Input = String
    typealias Failure = Never

    private var subscription: Subscription?

    func receive(subscription: Subscription) {
        self.subscription = subscription
        subscription.request(.unlimited)
    }

    func receive(_ input: String) -> Subscribers.Demand {
        print("Received data in class subscriber: \(input)")
        return .none
    }

    func receive(completion: Subscribers.Completion<Never>) {
        print("Data stream completed in class subscriber.")
    }
}

let publisher = Just("Hello, Combine!")
let subscriber = MyClassSubscriber()

publisher.subscribe(subscriber)
```

在这两个示例中，我们分别创建了一个结构体和一个类，它们都实现了 `Subscriber` 协议。它们分别用于接收和处理来自 `Just` 发布者的数据流。虽然两者的功能相同，但结构体是值类型，类是引用类型，这是它们的主要区别。你可以根据你的需求选择使用其中之一。




## 22. 自定义 发布者Publisher和订阅Subsctription

**目标：**通过本节 ，学习如何 扩展发布者和订阅机制，以及如何实现自定义。
认识为什么需要自定义发布者（Publisher）和订阅(Subseription)
学习如何扩展发布者Publisher。
学习两个发布者Publisher和订阅Subseription的自定义实现。
学习Publisher缓存机制的设计。
学习如何定义Operator，也就是有上游（Upstream）发布者
灵活使用中转订阅者 Sink。


### 22.1 认识为什么需要自定义发布者（Publisher）和订阅(Subseription)

自定义发布者（Publisher）和订阅（Subscription）是 Combine 框架中的核心概念，它们为你提供了灵活性和控制来适应各种异步数据流处理的需求。以下是为什么需要自定义发布者和订阅的一些原因：

**1. 适应特定的数据源：** 自定义发布者允许你创建适用于特定数据源或数据流的数据处理逻辑。不同的数据源可能需要不同的订阅逻辑，自定义发布者能够满足这种差异性需求。

**2. 数据流转换：** 你可以创建自定义发布者来对数据流进行转换、筛选、合并等操作。这使你能够以声明式的方式处理数据流，而不需要大量的嵌套回调和异步处理代码。

**3. 错误处理：** 自定义发布者可以实现错误处理逻辑，例如将特定类型的错误转化为另一种类型的错误，或在出现错误时采取特定的操作。

**4. 自定义订阅逻辑：** 自定义订阅可以用于管理订阅的生命周期、限制数据的速率、实现缓存机制等。这些都是根据具体需求自定义订阅逻辑的例子。

**5. 与现有 API 集成：** 你可以自定义发布者以与现有的异步 API 集成。这使得使用 Combine 处理异步操作更加方便，而不需要修改原有代码。

**6. 高度灵活性：** 自定义发布者和订阅提供了极高的灵活性，让你能够精确控制数据流的行为。这对于处理复杂的业务逻辑和异步场景非常有用。

自定义发布者和订阅是 Combine 框架的核心构建块，它们使你能够创建高度可组合的数据流处理管道，同时也能适应不同的数据源和异步操作。无论是在 iOS、macOS、watchOS 还是 tvOS 开发中，自定义发布者和订阅都是构建响应式和异步应用程序的强大工具。



### 22.2 如何扩展发布者Publisher

要扩展 Combine 中的发布者（Publisher），你可以创建自定义发布者类型并实现 `Publisher` 协议。这允许你将自己的逻辑添加到数据流处理管道中。以下是一个简单的示例，展示如何扩展发布者以生成递增的整数序列：

```swift
import Combine

// 自定义发布者类型，遵守 Publisher 协议，指定发布的数据类型和错误类型
struct CustomPublisher: Publisher {
    typealias Output = Int
    typealias Failure = Never

    // 自定义发布者需要一个订阅逻辑
    func receive<S>(subscriber: S) where S : Subscriber, Failure == S.Failure, Output == S.Input {
        // 创建订阅对象并将其传递给订阅者
        let subscription = CustomSubscription(subscriber: subscriber)
        subscriber.receive(subscription: subscription)
    }
}

// 自定义订阅类型，遵守 Subscription 协议
class CustomSubscription<S: Subscriber>: Subscription where S.Input == Int, S.Failure == Never {
    private var subscriber: S
    private var currentValue = 0
    private var isCancelled = false

    init(subscriber: S) {
        self.subscriber = subscriber
    }

    func request(_ demand: Subscribers.Demand) {
        guard !isCancelled else { return }

        // 模拟递增的数据流
        for _ in 0..<demand {
            if isCancelled {
                break
            }
            currentValue += 1
            _ = subscriber.receive(currentValue)
        }
    }

    func cancel() {
        isCancelled = true
    }
}

// 使用自定义发布者
let customPublisher = CustomPublisher()
customPublisher.sink { value in
    print(value)
}

// 手动请求数据
customPublisher.request(.max(5))
```

在上述示例中，我们创建了一个名为 `CustomPublisher` 的自定义发布者，它发出递增的整数。该发布者使用自定义订阅对象 `CustomSubscription` 来管理数据流，并在请求数据时生成递增的整数。通过自定义发布者，你可以扩展 Combine 的功能，以适应特定需求。在实际应用中，你可以根据需要实现自定义发布者来处理各种不同的数据源和逻辑。



### 22.3 发布者Publisher和订阅Subseription的自定义实现

为了自定义 Combine 中的订阅者（Subscriber）、发布者（Publisher）和订阅（Subscription），你需要实现相应的协议，并按照自定义逻辑来处理数据流。以下是一个自定义发布者、订阅者和订阅的示例：

**自定义发布者（Custom Publisher）**：

首先，创建一个自定义发布者类型，遵守 `Publisher` 协议，并指定输出和错误类型。在 `receive(subscriber:)` 方法中，你需要创建一个自定义订阅对象并将其传递给订阅者：

```swift
import Combine

struct CustomPublisher: Publisher {
    typealias Output = Int
    typealias Failure = Never

    func receive<S>(subscriber: S) where S : Subscriber, Failure == S.Failure, Output == S.Input {
        let subscription = CustomSubscription(subscriber: subscriber)
        subscriber.receive(subscription: subscription)
    }
}
```

**自定义订阅（Custom Subscription）**：

然后，创建一个自定义订阅类型，遵守 `Subscription` 协议，并实现 `request(_:)` 和 `cancel()` 方法来处理订阅逻辑。这里，我们模拟一个递增的整数序列：

```swift
class CustomSubscription<S: Subscriber>: Subscription where S.Input == Int, S.Failure == Never {
    private var subscriber: S
    private var currentValue = 0
    private var isCancelled = false

    init(subscriber: S) {
        self.subscriber = subscriber
    }

    func request(_ demand: Subscribers.Demand) {
        guard !isCancelled else { return }

        for _ in 0..<demand {
            if isCancelled {
                break
            }
            currentValue += 1
            _ = subscriber.receive(currentValue)
        }
    }

    func cancel() {
        isCancelled = true
    }
}
```

**自定义订阅者（Custom Subscriber）**：

最后，你可以创建一个自定义订阅者类型，遵守 `Subscriber` 协议，并实现 `receive(subscription:)`, `receive(_:)`, 和 `receive(completion:)` 方法来处理数据流。在这里，我们简单地打印接收到的数据：

```swift
struct CustomSubscriber: Subscriber {
    typealias Input = Int
    typealias Failure = Never

    func receive(subscription: Subscription) {
        subscription.request(.unlimited)
    }

    func receive(_ input: Int) -> Subscribers.Demand {
        print("Received data: \(input)")
        return .unlimited
    }

    func receive(completion: Subscribers.Completion<Never>) {
        print("Data stream completed.")
    }
}
```

现在，你可以使用自定义发布者、订阅者和订阅来创建一个自定义的数据流处理管道：

```swift
let customPublisher = CustomPublisher()
let customSubscriber = CustomSubscriber()

customPublisher.subscribe(customSubscriber)

// 手动请求数据
customPublisher.request(.max(5))
```

这个示例演示了如何自定义发布者、订阅者和订阅来处理数据流。你可以根据自己的需求扩展和自定义这些组件以满足特定的数据流处理逻辑。



### 22.4 Publisher缓存机制的设计

在 Combine 中，可以通过自定义订阅者（Subscriber）来实现缓存机制。缓存机制可以用于缓存和重播已接收的数据，以便在需要时再次访问。下面是一个简单的示例，展示如何创建一个具有缓存机制的自定义发布者：

```swift
import Combine

class CachedPublisher: Publisher {
    typealias Output = Int
    typealias Failure = Never

    private let originalPublisher: AnyPublisher<Output, Failure>
    private var cachedValues: [Int] = []
    private var subscriber: AnySubscriber<Output, Failure>?

    init() {
        // 创建一个原始的发布者，这里使用 Just 作为示例
        originalPublisher = Just(1)
            .merge(with: Just(2))
            .merge(with: Just(3))
    }

    func receive<S>(subscriber: S) where S : Subscriber, Failure == S.Failure, Output == S.Input {
        // 创建一个自定义订阅对象
        let subscription = CachedSubscription(subscriber: subscriber, cachedValues: cachedValues, originalPublisher: originalPublisher)
        subscriber.receive(subscription: subscription)
    }

    // 自定义订阅对象
    private class CachedSubscription<S: Subscriber>: Subscription where S.Input == Output, S.Failure == Failure {
        private var subscriber: S?
        private var cachedValues: [Int]
        private var originalPublisher: AnyPublisher<Output, Failure>?
        private var demand: Subscribers.Demand = .none

        init(subscriber: S, cachedValues: [Int], originalPublisher: AnyPublisher<Output, Failure>) {
            self.subscriber = subscriber
            self.cachedValues = cachedValues
            self.originalPublisher = originalPublisher
        }

        func request(_ demand: Subscribers.Demand) {
            self.demand += demand
            // 如果有需求，尝试从缓存中发送数据
            while self.demand > 0, let value = cachedValues.first {
                self.demand -= 1
                cachedValues.removeFirst()
                _ = subscriber?.receive(value)
            }
            // 如果缓存中没有足够的数据，向原始发布者请求数据
            if self.demand > 0 {
                let subscription = originalPublisher?.sink(receiveValue: { [weak self] value in
                    guard let self = self else { return }
                    self.cachedValues.append(value)
                    if self.demand > 0 {
                        self.demand -= 1
                        _ = self.subscriber?.receive(value)
                    }
                })
                // 记得取消原始发布者的订阅以避免内存泄漏
                _ = subscription
            }
        }

        func cancel() {
            subscriber = nil
            originalPublisher = nil
        }
    }
}

// 使用自定义发布者和订阅者
let cachedPublisher = CachedPublisher()
let subscriber = AnySubscriber<Int, Never>(receiveSubscription: { subscription in
    subscription.request(.unlimited)
}, receiveValue: { value in
    print("Received value: \(value)")
    return .unlimited
}, receiveCompletion: { _ in })

cachedPublisher.subscribe(subscriber)
```

在这个示例中，`CachedPublisher` 是一个具有缓存机制的自定义发布者。当订阅者请求数据时，它首先检查缓存，如果缓存中有足够的数据，则从缓存中发送；否则，它向原始发布者请求数据，并将收到的数据缓存在 `cachedValues` 中，以便下次使用。这个示例演示了如何自定义发布者来实现简单的缓存机制，你可以根据需要扩展和改进这个机制。



### 22.5 如何定义Operator，也就是有上游（Upstream）发布者

在 Combine 中，你可以创建自定义操作符（Operator），这些操作符可以处理上游（Upstream）发布者产生的数据并生成下游（Downstream）发布者。为了定义一个操作符，你需要创建一个扩展（extension）来添加方法到 `Publisher`，其中包含你的自定义操作符逻辑。以下是一个简单的示例，展示如何定义一个自定义操作符来过滤出偶数：

```swift
import Combine

extension Publisher {
    func filterEvenNumbers() -> AnyPublisher<Output, Failure> {
        return self.compactMap { value in
            // 过滤出偶数
            if value % 2 == 0 {
                return value
            }
            return nil
        }.eraseToAnyPublisher()
    }
}

// 创建一个发布者
let numbersPublisher = [1, 2, 3, 4, 5, 6].publisher

// 使用自定义操作符来过滤出偶数
let evenNumbersPublisher = numbersPublisher.filterEvenNumbers()

// 订阅并输出过滤后的结果
evenNumbersPublisher.sink { value in
    print("Received even number: \(value)")
}
```

在上述示例中，我们扩展了 `Publisher` 并添加了一个名为 `filterEvenNumbers()` 的自定义操作符。该操作符使用 `compactMap` 来过滤出偶数，并使用 `eraseToAnyPublisher()` 来返回一个新的发布者。然后，我们使用自定义操作符来过滤出偶数并进行订阅。

你可以根据需要创建各种自定义操作符，用于数据转换、过滤、合并、映射等操作。这些操作符可以让你以声明式的方式构建数据流处理管道。



### 22.6 灵活使用中转订阅者 Sink

`Sink` 是 Combine 中用于接收发布者的最常用的订阅者（Subscriber），它让你能够订阅发布者并处理其输出值、完成事件以及错误事件。你可以通过 `sink` 方法来创建 `Sink` 订阅者。以下是一些示例，展示如何在实际应用中灵活使用 `Sink` 订阅者：

**1. 接收并处理值：**

```swift
import Combine

let publisher = [1, 2, 3, 4, 5].publisher

let cancellable = publisher.sink { value in
    print("Received value: \(value)")
}

// 注意：sink 返回一个 Cancellable 对象，可以用于取消订阅
```

**2. 处理完成事件：**

```swift
import Combine

let publisher = Just("Hello, Combine!")

let cancellable = publisher.sink(
    receiveValue: { value in
        print("Received value: \(value)")
    },
    receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Data stream completed successfully.")
        case .failure(let error):
            print("Data stream failed with error: \(error)")
        }
    }
)
```

**3. 处理错误事件：**

```swift
import Combine

let publisher = Fail<Int, Error>(error: MyError.customError)

let cancellable = publisher.sink(
    receiveValue: { value in
        print("Received value: \(value)")
    },
    receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Data stream completed successfully.")
        case .failure(let error):
            print("Data stream failed with error: \(error)")
        }
    }
)
```

**4. 取消订阅：**

你可以使用 `Cancellable` 对象来取消订阅，以停止接收发布者的事件：

```swift
let cancellable = publisher.sink { value in
    print("Received value: \(value)")
}

// 取消订阅
cancellable.cancel()
```

使用 `Sink` 订阅者，你可以非常灵活地处理发布者产生的事件，包括接收值、处理完成事件和处理错误事件。这使得它成为 Combine 中非常重要和实用的工具。




## 23. Backpressure概念以及对应方法

**目标：**理解subscription.request的意义。

Subscriber的订阅对象重启方法。
学习Subscribeis.Demnand的使用。
学习Publisher的声明式sink定义。
理解Subscribers.Demand关 于 backpressure 的 处理流程设计。


"Backpressure" 是一种流控制的概念，通常用于异步编程和数据流处理中，以处理生产者（Producer）和消费者（Consumer）之间的速率不匹配。当生产者生成的数据速度远快于消费者处理数据的速度时，可能会出现数据积压的问题。"Backpressure" 就是一种机制，用于调整或限制数据流的速率，以确保消费者不被淹没并能够处理数据。

在 Combine 中，"Backpressure" 通常通过以下方式来处理：

1. **Demand（需求）：** 每个订阅者（Subscriber）都会向发布者（Publisher）发送一个 "需求"，表示它可以接收多少个数据元素。发布者会根据这个需求来发送数据。这有助于控制数据流的速率。

2. **缓冲区：** 一些发布者可以具有缓冲区，用于存储尚未处理的数据元素。订阅者可以按照其自己的速率来处理数据，而不必等待数据的生成。

3. **合并与压缩：** 使用一些操作符，如 `merge` 或 `combineLatest`，可以将多个发布者的数据合并成一个，从而减小数据流的数量，减轻数据积压的问题。

4. **Throttle 和 Debounce：** 这些操作符可以用于减缓数据流，以便在一段时间内或在特定条件下发送数据。

5. **Retry 和 RetryWhen：** 这些操作符允许在遇到错误时重试数据流，以确保数据被成功处理。

请注意，Combine 已经在设计中考虑到了 "Backpressure"，并使用 Demand 来控制数据流的速率。在许多情况下，你可以使用 Combine 的默认行为来处理 "Backpressure"，但也可以使用操作符和自定义订阅者来进一步调整数据流的速率，以满足特定需求。



### 23.1 Subscriber的订阅对象重启方法

在 Combine 中，Subscriber 订阅对象无法直接执行重启（重新订阅）的方法。一旦订阅者（Subscriber）完成了对发布者（Publisher）的订阅，订阅对象会被销毁，而且 Combine 框架没有提供内置的方法来重新订阅。

如果你需要在某些情况下重新订阅发布者，你可以考虑以下两种方法：

1. **创建一个新的订阅者对象：** 你可以简单地创建一个新的订阅者对象并将其订阅到相同的发布者上，以达到重新订阅的效果。这是 Combine 中常见的做法。

   ```swift
   let publisher = ... // 创建你的发布者
   let subscriber = MySubscriber() // 创建一个新的订阅者对象
   publisher.subscribe(subscriber) // 订阅发布者
   ```

2. **使用 Operators 和 Publishers：** Combine 提供了许多操作符和发布者，允许你以不同的方式处理数据流。你可以使用这些操作符来重新定义你的数据流处理逻辑，而不必重新订阅。

   ```swift
   let publisher = ... // 创建你的发布者
   let modifiedPublisher = publisher
       .map { ... } // 使用 map 进行数据转换
       .filter { ... } // 使用 filter 进行数据过滤
   ```

通常情况下，第一种方法更加直观，而第二种方法更加灵活，具体取决于你的需求。 Combine 的强大之处在于，你可以使用操作符来构建复杂的数据流处理管道，而不必重新订阅。如果需要重启整个数据流，可以创建一个新的订阅者对象并将其订阅到发布者上。



### 23.2 Subscribeis.Demnand的使用
`Subscribers.Demand` 是 Combine 中的一个关键类型，用于表示订阅者（Subscriber）的需求，即它可以接收多少个数据元素。理解和正确使用 `Subscribers.Demand` 对于管理数据流的速率和处理数据的顺序至关重要。

`Subscribers.Demand` 主要用于两个地方：

1. **在订阅者中使用 `request(_:)`：** 订阅者可以通过调用 `request(_:)` 方法向发布者请求一定数量的数据元素。这是数据流速率控制的关键。`request(_:)` 的参数是一个 `Subscribers.Demand` 对象，表示订阅者的需求。例如，如果一个订阅者请求了 `.unlimited`，则表示它可以接收无限数量的数据元素，而如果请求了 `.max(10)`，则表示它最多可以接收 10 个数据元素。

   ```swift
   subscription.request(.max(5)) // 请求最多 5 个数据元素
   ```

2. **在发布者中使用 `receive(_:)`：** 发布者在发送数据元素时，会检查订阅者的需求，并仅发送符合需求数量的数据元素。这有助于确保数据流不会淹没订阅者。

理解 `Subscribers.Demand` 的使用有助于优化数据流处理，防止数据积压或过度发送数据。在编写自定义操作符或订阅者时，你需要根据订阅者的需求来控制数据的发送速率，以提高性能和避免资源浪费。

下面是一些 `Subscribers.Demand` 的常见用法示例：

```swift
let demand1: Subscribers.Demand = .max(10) // 请求最多 10 个数据元素
let demand2: Subscribers.Demand = .unlimited // 请求无限数量的数据元素

// 计算需求的总和
let totalDemand = demand1 + demand2 // 结果是 .max(10)
```

通过合理使用 `Subscribers.Demand`，你可以更好地管理 Combine 数据流，确保数据以合适的速率被处理。



### 23.3 Publisher的声明式sink定义

在 Combine 中，`sink` 不是一个声明式操作符，而是一种用于订阅和处理数据流的订阅者（Subscriber）的方法。它通常用于执行副作用和处理发布者（Publisher）产生的值、完成事件或错误事件。通常，`sink` 方法在数据流处理链的最末端被使用，以触发数据流的执行。

以下是 `sink` 方法的一般定义：

```swift
func sink(receiveCompletion: @escaping (Subscribers.Completion<Failure>) -> Void, 
          receiveValue: @escaping (Output) -> Void) -> AnyCancellable
```

- `receiveCompletion` 参数是一个闭包，用于处理完成事件，它接收一个 `Subscribers.Completion` 枚举，可以是 `.finished`（数据流成功完成）或 `.failure`（数据流出现错误）。

- `receiveValue` 参数是一个闭包，用于处理每个产生的值，它接收发布者发送的每个数据元素。

- `AnyCancellable` 是 `sink` 方法的返回值，用于订阅。你可以保持对返回的 `AnyCancellable` 对象的引用，以便稍后取消订阅。

以下是一个示例使用 `sink` 方法的情况：

```swift
import Combine

let publisher = Just("Hello, Combine!")

let cancellable = publisher.sink(
    receiveValue: { value in
        print("Received value: \(value)")
    },
    receiveCompletion: { completion in
        switch completion {
        case .finished:
            print("Data stream completed successfully.")
        case .failure(let error):
            print("Data stream failed with error: \(error)")
        }
    }
)

// 注意：保持对 cancellable 的引用，以便稍后取消订阅
```

在上述示例中，我们使用 `sink` 方法来订阅 `publisher`，并定义了闭包来处理值和完成事件。一旦完成事件发生或者取消订阅，可以通过保持对 `cancellable` 对象的引用来释放资源。

尽管 `sink` 不是一个声明式操作符，但它是 Combine 中非常有用的工具，用于执行数据流处理的最终操作和副作用。



### 23.4 Subscribers.Demand关于 backpressure 的处理流程设计
在 Combine 中，`Subscribers.Demand` 是用于处理 backpressure（背压）的关键机制之一。背压是指当生产者（Publisher）生成数据的速度远快于消费者（Subscriber）处理数据的速度时，需要一种机制来限制或调整数据流的速率，以避免数据积压或资源耗尽。`Subscribers.Demand` 的主要作用是表示消费者可以接受的数据元素数量。

以下是 `Subscribers.Demand` 与 backpressure 处理的关键流程设计：

1. **消费者向发布者发送需求：** 每个消费者（Subscriber）在订阅时可以向发布者（Publisher）发送需求，表示它可以接受多少个数据元素。需求可以是 `.max(n)`，表示最多接受 n 个元素，也可以是 `.unlimited`，表示无限制。

2. **发布者根据需求发送数据：** 发布者在发送数据时会检查订阅者的需求，并只发送符合需求数量的数据元素。如果需求是 `.max(n)`，则发布者只会发送最多 n 个元素。

3. **需求的动态变化：** 随着数据的处理，消费者可以通过调用 `request(_:)` 方法来更改其需求。这允许消费者根据处理速率来调整需求。

4. **数据流的速率控制：** 发布者在发送数据时会根据订阅者的需求来控制数据流的速率。这确保了数据不会被发送得太快而导致积压。

以下是一个示例，展示了如何使用 `Subscribers.Demand` 处理 backpressure：

```swift
import Combine

let publisher = (1...10).publisher

let subscriber = Subscribers.Sink<Int, Never>(
    receiveCompletion: { completion in
        print("Data stream completed with \(completion).")
    },
    receiveValue: { value in
        print("Received value: \(value)")
    }
)

publisher.subscribe(subscriber)

// 初始需求是 .unlimited，可以接受无限数据
subscriber.receive(subscription: Subscriptions.empty)

// 需求变为 .max(5)，限制接受最多 5 个数据元素
subscriber.receive(request: .max(5))
```

在上述示例中，订阅者首先订阅了发布者，并使用 `receive(subscription:)` 方法来接受初始需求为 `.unlimited`，表示可以接受无限数据。然后，它通过 `receive(request:)` 方法将需求更改为 `.max(5)`，从而限制了只接受最多 5 个数据元素。这样，数据流的速率得以控制。

使用 `Subscribers.Demand` 可以使 Combine 在处理数据流时更具灵活性，避免数据积压和资源耗尽的问题。消费者可以根据自身处理速率来动态调整需求，以满足背压的需求。


