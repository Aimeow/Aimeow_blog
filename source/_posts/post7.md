title: iOS日志框架CocoaLumberjack配置
date: 2015-05-26 10:23:06
tags:
---
首先，你想要在你的应用程序中配置这个日志框架，通常在applicationDidFinishLaunching方法中配置。
开始时，你需要下面两行代码：
```c++
[DDLog addLogger:[DDASLLogger sharedInstance]]; 
[DDLog addLogger:[DDTTYLogger sharedInstance]]; 
```
这将在你的日志框架中添加两个“logger”。也就是说你的日志语句将被发送到Console.app和Xcode控制 台（就像标准的NSLog）
这个框架的好处之一就是它的灵活性，如果你还想要你的日志语句写入到一个文件中，你可以添加和配置一个file logger:
```c++
fileLogger = [[DDFileLogger alloc] init]; 
fileLogger.rollingFrequency = 60 * 60 * 24; // 24 hour rolling 
fileLogger.logFileManager.maximumNumberOfLogFiles = 7; 
[DDLog addLogger:fileLogger];   
```
上面的代码告诉应用程序要在系统上保持一周的日志文件。
用DDLog替换NSLog语句 DDLog的头文件定义了你用来替换NSLog语句的宏，本质上看起来向下边这样：
```c++
// Convert from this: 
NSLog(@"Broken sprocket detected!"); 
NSLog(@"User selected file:%@ withSize:%u", filePath, fileSize); 
    
// To this: 
DDLogError(@"Broken sprocket detected!"); 
DDLogVerbose(@"User selected file:%@ withSize:%u", filePath, fileSize); 
```
我们看到DDLog宏和NSLog的语法完全相同。
所以你所要做的就是决定每个NSlog语句属于哪种日志级别。DDLog默认有四种级别的日志，分别是： 1.@DDlogError 
2.@DDlogWarn 
3.@DDlogInfo 
4.@DDlogVerbose
在配置CocoaLumberjack前可以通过Alcatraz安装XcodeColors,若控制台输出的文字仍然还是黑色，则可以通过
```c++
 product->scheme->Edit Scheme->Run->Argument->Environment Variables
```
加上XcodeColors : YES,然后重启Xcode即可。