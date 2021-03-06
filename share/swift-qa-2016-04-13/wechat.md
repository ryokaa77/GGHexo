每周 Swift 社区问答：@available 和 #available"


Swift 2.0 中，引入了可用性的概念。对于函数，类，协议等，可以使用`@available`声明这些类型的生命周期依赖于特定的平台和操作系统版本。而`#available`用在判断语句中（if, guard, while等），在不同的平台上做不同的逻辑。



## @available

### 用法

`@available`放在函数（方法），类或者协议前面。表明这些类型适用的平台和操作系统。看下面一个例子：

    @available(iOS 9, *)
    func myMethod() {
        // do something
    }
`@available(iOS 9, *)`必须包含至少2个特性参数，其中`iOS 9`表示必须在 iOS 9 版本以上才可用。如果你部署的平台包括 iOS 8 , 在调用此方法后，编译器会报错。
另外一个特性参数：星号（*），表示包含了所有平台，目前有以下几个平台：

* iOS
* iOSApplicationExtension
* OSX
* OSXApplicationExtension
* watchOS
* watchOSApplicationExtension
* tvOS
* tvOSApplicationExtension

一般来讲，如果没有特殊的情况，都使用`*`表示全平台。

`@available(iOS 9, *)`是一种简写形式。全写形式是`@available(iOS, introduced=9.0)`。`introduced=9.0`参数表示指定平台(iOS)从 9.0 开始引入该声明。为什么可以采用简写形式呢？当只有`introduced`这样一种参数时，就可以简写成以上简写形式。同理：@available(iOS 8.0, OSX 10.10, *) 这样也是可以的。表示同时在多个平台上（iOS 8.0 及其以上；OSX 10.10及其以上）的可用性。

另外，`@available`还有其他一些参数可以使用，分别是：

* `deprecated=版本号`：从指定平台某个版本开始过期该声明
* `obsoleted=版本号`：从指定平台某个版本开始废弃（注意弃用的区别，`deprecated`是还可以继续使用，只不过是不推荐了，`obsoleted`是调用就会编译错误）该声明
* `message=信息内容`：给出一些附加信息
* `unavailable`：指定平台上是无效的
* `renamed=新名字`：重命名声明

以上参数具体可以参考[官方文档](http://wiki.jikexueyuan.com/project/swift/chapter3/06_Attributes.html)





## #available

`#available` 用在条件语句代码块中，判断不同的平台下，做不同的逻辑处理，比如：

    if #available(iOS 8, *) {
            // iOS 8 及其以上系统运行
    }
    
    
    guard #available(iOS 8, *) else {
        return //iOS 8 以下系统就直接返回
    }

### stackoverflow 相关问题整理

* [Difference between @available and #available in swift 2.0](http://stackoverflow.com/questions/32761511/difference-between-available-and-available-in-swift-2-0): @available 和 #available
帖子里面还提到一个问题：`@available`是编译期间判断的吗？而`#available`是运行时行为吗？




### 参考资料
* [API Availability Checking in Swift 2](http://www.codingexplorer.com/api-availability-checking-in-swift-2/)
* [Availability checking in Swift 2: backwards compatibility the smart way](https://www.hackingwithswift.com/new-syntax-swift-2-availability-checking)






