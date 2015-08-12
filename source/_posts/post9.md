title: 用GDB命令PO（print-object）打印UIView的视图层级
date: 2015-05-26 10:31:41
tags:
---
UIView有一个私有方法：recursiveDescription 
这个方法可以显示出当前视图的详细层级，可以在代码中直接调用，也可以在GDB中调用，在GDB中调用时需要借助另一个GDB命令：print-object：
```c++
  po [self.view recursiveDescription]
```