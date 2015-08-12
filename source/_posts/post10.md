title: 查看iOS设备支持的字体
date: 2015-05-26 10:32:26
tags:
---
可以通过遍历UIFont中的familyNames得到所有iOS设备的字体
```c++
for (NSString *family in [UIFont familyNames]) 
{ 
	NSLog(@"%@", family); 
	for(NSString *font in [UIFont fontNamesForFamilyName:family]) 
	{ 
		NSLog(@"\t%@",font); 
	} 
} 
```