title: iOS获取当前屏幕截屏
date: 2015-05-26 10:33:17
tags:
---
```c++
- (UIImage *)getScreenShot { 
	UIGraphicsBeginImageContext(self.view.bounds.size); 
	[self.view.layer renderInContext:UIGraphicsGetCurrentContext()]; 
	UIImage *image = UIGraphicsGetImageFromCurrentImageContext(); 
	UIGraphicsEndImageContext(); 
	return image; 
} 
```