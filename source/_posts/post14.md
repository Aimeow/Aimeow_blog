title: objc runtime 动态增加属性
date: 2015-05-26 10:38:50
tags:
---
objective-c中，有类别可以在不修改源码的基础上增加方法；近排在看别人的开源代码时，发现还可以动态增加属性。而且是在运行时,太牛B了。
使用运行时库，必须要先引入 objc/runtime.h
可以使用的函数如下：
```c++
OBJC_EXPORT void objc_setAssociatedObject(id object, const void *key, id value, objc_AssociationPolicy policy)
```
这个函数
```c++
OBJC_EXPORT id objc_getAssociatedObject(id object, const void *key)
__OSX_AVAILABLE_STARTING(__MAC_10_6, __IPHONE_3_1);
```
兄弟们，看一个类别和动态添加属性的例子：

UILabel+Associate.h
```c++
#import <UIKit/UIKit.h>
    
@interface UILabel (Associate)
    
- (void) setFlashColor:(UIColor *) flashColor;
    
- (UIColor *) getFlashColor;
    
@end
```
UILabel+Associate.m
```c++
#import "UILabel+Associate.h"
#import <objc/runtime.h>
    
@implementation UILabel (Associate)
    
static char flashColorKey;
    
- (void) setFlashColor:(UIColor *) flashColor{
	objc_setAssociatedObject(self, &flashColorKey, flashColor, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
}
    
- (UIColor *) getFlashColor{
	return objc_getAssociatedObject(self, &flashColorKey);
}
@end
```
调用代码：
```c++
UILabel *lab = [[UILabel alloc] init];
[lab setFlashColor:[UIColor redColor]];
NSLog(@"%@", [lab getFlashColor]);
```
转自:http://www.cnblogs.com/luoguoqiang1985/p/3551966.html?utm_source=tuicool