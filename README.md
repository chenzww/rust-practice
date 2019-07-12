# Rust语言学习笔记

## [Rust概述](https://mp.weixin.qq.com/s?__biz=MzA5NTQyNDIyNw==&mid=2247483774&idx=1&sn=0f76ebdaf945da8f28c7753d9fd4399a)

摘录片段：
Rust代码非常接近自然语言。

```Rust
5.times(|| println!("Hello Rust"));
2.days().from_now();
```
## [Rust基本语法](https://mp.weixin.qq.com/s?__biz=MzA5NTQyNDIyNw==&mid=2247483778&idx=1&sn=52c655fb8bbc81eaaa0ce2acc1c9d07f)

Rust一切皆表达式。

个人觉得闭包降低了代码的可读性，一段好的代码，要有良好的阅读体验，而不是写的时候方便。

### 练习代码

* [Rust表达式](https://github.com/lesterli/rust-practice/blob/master/src/statement.rs)
* [Rust变量](https://github.com/lesterli/rust-practice/blob/master/src/variable.rs)
* [Rust函数](https://github.com/lesterli/rust-practice/blob/master/src/function.rs)
* [Rust流程控制](https://github.com/lesterli/rust-practice/blob/master/src/control_flow.rs)

## [Rust数据类型](https://mp.weixin.qq.com/s?__biz=MzA5NTQyNDIyNw==&mid=2247483783&idx=1&sn=8625be095bdcc56758136cd837e5b107)

利用元组，函数可以返回多个值。

什么是字符串？

Rust原始的字符串类型：`str`，它是固定长度的。

字符串切片slice：`&str`，它是储存在别处的UTF-8编码字符串数据的引用。

而称作`String`类型的字符串是由标准库提供的，它是可增长的、可变长度的、有所有权的、UTF-8编码的字符串类型。

### 练习代码

* [Rust原始类型](https://github.com/lesterli/rust-practice/blob/master/src/primitives.rs)
* [Rust集合类型](https://github.com/lesterli/rust-practice/blob/master/src/collections.rs)

## [Rust核心概念](https://mp.weixin.qq.com/s?__biz=MzA5NTQyNDIyNw==&mid=2247483787&idx=1&sn=a4cfc40e7ae380cbb2d7bf091d71a4ec)

### 类型系统

Rust是一门强类型且类型安全的静态语言。

一个类型系统允许一段代码在不同上下文中具有不同的类型，多态类型系统。三种多态方式：

* 参数化多态，泛型
* 子类型多态，面向对象语言，Java中的继承概念
* 特定多态，同一行为定义，不同上下文中有不同的行为实现，函数重载

`trait`的概念：它是Rust中提供的一种实现特定多态的方法，类似于其他语言中的接口（interfaces）。

### 所有权系统

所有权的规则：

* Rust中的每一个值，都有一个被称为其所有者（owner）的变量
* 值有且只有一个所有者
* 当所有者（变量）离开作用域，这个值将被丢弃

所有权转移，一个值的所有权被转移给另外一个变量绑定的过程。

复制语义和移动语义来对应值语义和引用语义。实现`Copy trait`的类型拥有复制语义。

移动move语义：一个旧的变量（数据存在堆上）在将其赋值给其他变量后，意味着它的所有权被移动了。

### 模块系统

包`crate`的概念：crate代表一个二进制或库项目，用crate root来描述如何构建这个crate的文件。

### 错误处理

使用`Result`类型来处理潜在的错误。Result枚举，它定义有两个成员，Ok和Err：

```Rust
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```
### Rust并发

创建一个新线程，调用`thread::spawn`函数并传递一个闭包，其重包含希望在新线程运行的代码。

一个确保安全并发的方式是消息传递（message passing），线程通过发送包含数据的消息来相互通信。

> “Do not communicate by sharing memory; instead, share memory by communicating.”

通道（channel）来实现消息传递，创建通道，使用`mpsc::channel`函数。

不允许在线程间直接传递引用，那如何在多个线程间安全地共享变量呢？

不可变的变量，通过`Arc<T>`来共享，它是`Rc<T>`的线程安全版本，其内部使用了原子操作。

有两个并发概念是内嵌于语言中的：`std::marker`中的`Sync`和`Send` trait，使得并发保证能被扩展到用户定义的和标准库中提供的类型中。

### 练习代码

* [Rust类型系统](https://github.com/lesterli/rust-practice/blob/master/src/generics_trait.rs)
* [Rust所有权系统]()
* [Rust并发]()
