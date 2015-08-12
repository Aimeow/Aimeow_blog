title: id ,NSObject, id<NSObject>区别
date: 2015-05-28 15:47:46
tags:
---
我们经常会混淆以下三种申明（我是没有留意过）：
1. id foo1;
2. NSObject *foo2;
3. id<NSObject> foo3;

第一种是最常用的，它简单地申明了指向对象的指针，没有给编译器任何类型信息，因此，编译器不会做类型检查。但也因为是这样，你可以发送任何信息给id类型的对象。这就是为什么+alloc返回id类型，但调用[[Foo alloc] init]不会产生编译错误。

因此，id类型是运行时的动态类型，编译器无法知道它的真实类型，即使你发送一个id类型没有的方法，也不会产生编译警告。

我们知道，id类型是一个Objective-C对象，但并不是都指向继承自NSOjbect的对象，即使这个类型和NSObject对象有很多共同的方法，像retain和release。要让编译器知道这个类继承自NSObject，一种解决办法就是像第2种那样，使用NSObject静态类型，当你发送NSObject没有的方法，像length或者count时，编译器就会给出警告。这也意味着，你可以安全地使用像retain，release，description这些方法。

因此，申明一个通用的NSObject对象指针和你在其它语言里做的类似，像java，但其它语言有一定的限制，没有像Objective-C这样灵活。并不是所有的Foundation/Cocoa对象都继承息NSObject，比如NSProxy就不从NSObject继承，所以你无法使用NSObject＊指向这个对象，即使NSProxy对象有release和retain这样的通用方法。为了解决这个问题，这时候，你就需要一个指向拥有NSObject方法对象的指针，这就是第3种申明的使用情景。

id<NSObject>告诉编译器，你不关心对象是什么类型，但它必须遵守NSObject协议(protocol)，编译器就能保证所有赋值给id<NSObject>类型的对象都遵守NSObject协议(protocol)。这样的指针可以指向任何NSObject对象，因为NSObject对象遵守NSObject协议(protocol)，而且，它也可以用来保存NSProxy对象，因为它也遵守NSObject协议(protocol)。这是非常强大，方便且灵活，你不用关心对象是什么类型，而只关心它实现了哪些方法。

现在你知道你要用什么类型了不？

如果你不需要任何的类型检查，使用id，它经常作为返回类型，也经常用于申明代理(delegate)类型。因为代理类型通常在运行时，才会检查是否实现了那些方法。

如果真的需要编译器检查，那你就考虑使用第2种或者第3种。很少看到NSObject＊能正常运行，但id<NSObject>无法正常运行的。使用协议(protocol)的优点是，它能指向NSProxy对象，而更常用的情况是，你只想知道某个对象遵守了哪个协议，而不用关心它是什么类型。