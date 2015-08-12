title: Reveal查看任意app的高级技巧
date: 2015-05-27 09:48:59
tags:
---
Reveal是一个很强大的UI分析工具，与其他几个功能相近的工具（比如PonyDebugger）相比，其最大的特点就是非常直观，用来查看app的UI布局非常方便。其常规用法是将framework集成至Xcode工程中，可参见Reveal的官网<a href="http://revealapp.com/">http://revealapp.com/</a>,但我们这次讲述的却是非常规用法。
在12/21的#阿里技术嘉年华#上，我给听众展示了使用Reveal查看任意app的效果，估计是当时所展示的工具中最亮眼的一个。既然如此，我就提前在这里把Reveal的这个技巧详细的列出来。
1、越狱设备，iPhone/iTouch/iPad都可以，iOS6以上（惊闻iOS7也已经越狱了）；
2、安装Reveal，Trail或正式版都可以，然后越狱设备与安装Reveal的Mac在同一wifi内。
3、点击菜单Help / Show Reveal Library in Finder，获取libReveal.dylib
<img src="http://aimeow.qiniudn.com/003J6gH0zy6FcllcFF365.png"/>
4、将libReveal.dylib上传到设备的/Library/MobileSubstrate/DynamicLibraries
<img src="http://aimeow.qiniudn.com/003J6gH0zy6FclUuvMqa6.png"/>
5、同时编辑并上传一个libReveal.plist，格式如下：
<img src="http://aimeow.qiniudn.com/003J6gH0zy6FcmaO2Fye8.png"/>
注意，此时是可以指定多个BundleID的，也就是说，你可以同时监控任意多的app；再扩大一步说，如果你愿意，不上传这个libReveal.plist，你可以监控所有app，只要你不觉得机器很慢。。。
6、re-spring或重启iOS设备，打开你想看的app，再从Reveal界面左上角选择要连接的机器，进入不同的页面之后还可以点击右上角的刷新钮来刷新监测的页面信息。
<img src="http://aimeow.qiniudn.com/003J6gH0zy6Fcmplk8mfe.jpg"/>
以上是不写一行代码就能够查看任意app的方法，各位看别人app爽的时候，也可以摸摸脖子想想自己的app。
这种“高级技巧”从来没有被Reveal官方提起过，而是我们接触到Reveal之后逐步发现的。一开始的方法比较粗暴，是直接hook想看的app，把libReveal.dylib插进去；后来经过@卢明华 的进一步探索，才总结出这个更简单粗暴的方法。
虽然Reveal是最直观的一个工具，但是在iOS逆向这个领域，它占的比重连1/10都不到，真正的大块头都有点难啃，相信各位都是理解的。
最后，相信我们的书出来之后，会给朋友们更多深度撞击的感觉。


-----------------------
该文章转自http://c.blog.sina.com.cn/profile.php?blogid=cb8a22ea89000gtw