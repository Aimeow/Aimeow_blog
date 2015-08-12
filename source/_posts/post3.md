title: 对于UIColor的扩展（1）
date: 2015-05-26 10:14:58
tags:
---
官方UIColor的方法中，基本上都是通过RED,GREEN,BLUE三种色值去设置一种颜色。但很多时候，我们都是通过HEX值去设置一种颜色。所以我们可以通过方法去把HEX转换成我们需要的色值。
```c++
+ (UIColor *)colorwithHexString:(NSString *)hexString alpha:(float)alpha
{
    return [[self colorwithHexString:hexString] colorWithAlphaComponent:alpha];
}

+ (UIColor *)colorwithHexString:(NSString *)hexString
{
    if (hexString == nil || (id)hexString == [NSNull null]) {
        return nil;
    }
    UIColor *col;
    if (![hexString hasPrefix:@"#"]) {
        hexString = [NSString stringWithFormat:@"#%@", hexString];
    }
    hexString = [hexString stringByReplacingOccurrencesOfString:@"#"
                                                     withString:@"0x"];
    uint hexValue;
    if ([[NSScanner scannerWithString:hexString] scanHexInt:&hexValue]) {
        col = [UIColor
               colorWithRed:((float)((hexValue & 0xFF0000) >> 16))/255.0
               green:((float)((hexValue & 0xFF00) >> 8))/255.0
               blue:((float)(hexValue & 0xFF))/255.0
               alpha:1.0f];
    } else {
        col = [UIColor clearColor];
    }
    return col;
}


```
