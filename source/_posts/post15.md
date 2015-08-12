title: category使用 objc_setAssociatedObject/objc_getAssociatedObject 实现添加属性
date: 2015-05-26 10:42:05
tags:
---
属性 其实就是get/set 方法。我们可以使用 objcsetAssociatedObject/objcgetAssociatedObject 实现 动态向类中添加 方法
```c++
@interface NSObject (CategoryWithProperty)
    
@property (nonatomic, strong) NSObject *property;
    
@end
    
@implementation NSObject (CategoryWithProperty)
    
- (NSObject *)property {
	return objc_getAssociatedObject(self, @selector(property));
}
    
- (void)setProperty:(NSObject *)value {
	objc_setAssociatedObject(self, @selector(property), value, OBJC_ASSOCIATION_RETAIN_NONATOMIC);
}
    
@end
```