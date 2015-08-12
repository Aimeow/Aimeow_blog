title: 对于NSDictionary的扩展（1）
date: 2015-05-26 10:12:54
tags:
---
很多时候，在我们向服务端请求数据时，我们总会获取到一些值为NULL的数据。一旦出现这些数据，而客户端又未对其进行空值判断时，就会出现客户端崩溃的情况。为此，专门为这种情况对NSDictionary进行了扩展，使之可以安全的解析带NULL的数据。
``` c++
@interface NSDictionary (safe)

- (id)safeObjectForKey:(id)aKey;
- (NSString *)stringForKey:(id)aKey;
- (NSInteger)intForKey:(id)aKey;

@end
```
这个扩展实现了三个方法，分别对应从NSDictionary中取对象、字符串、还有数字类型的值。

``` c++
- (id)safeObjectForKey:(id)aKey
{
id object = [self objectForKey:aKey];
if (object == nil) {
object = @"";
}
return object;
}

```
当NSDictionary中取到的值如果为nil,则将其设为nil。后面两个方法同理。