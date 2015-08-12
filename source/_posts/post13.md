title: 关于willMoveToParentViewController和didMoveToParentViewController
date: 2015-05-26 10:34:42
tags:
---
iOS 5.0 后UIViewController新增：willMoveToParentViewController和didMoveToParentViewController
在iOS 5.0以前，我们在一个UIViewController中这样组织相关的UIView 在以前，一个UIViewController的View可能有很多小的子view。这些子view很多时候被盖在最后，我们在最外层ViewController的viewDidLoad方法中，用addSubview增加了大量的子view。这些子view大多数不会一直处于界面上，只是在某些情况下才会出现，例如登陆失败的提示view，上传附件成功的提示view，网络失败的提示view等。但是虽然这些view很少出现，但是我们却常常一直把它们放在内存中。另外，当收到内存警告时，我们只能自己手工把这些view从super view中去掉。
在iOS 5.0及以后，iOS为UIViewController类添加了新的属性和方法：
```c++
@property(nonatomic,readonly) NSArray *childViewControllers
    
- (void)addChildViewController:(UIViewController *)childController
- (void) removeFromParentViewController
- (void)transitionFromViewController：：：：：：
- (void)willMoveToParentViewController:(UIViewController *)parent
- (void)didMoveToParentViewController:(UIViewController *)parent
```
这样，就能够将一个页面中的UIViewController控制起来，而不是混乱的共用一个UIViewController，最重要的是，编程习惯的革命：降低了功能的耦合度！
写这篇博客，仅仅是讲以上5个方法！仅此而已。因为当我在百度或者谷歌中，输入以上5个方法的名字后，查出来的，并没有告诉这5个方法起到如何的作用？如何使用？
所以，我仅仅是想从API角度来谈一谈，这5个方法。
废话不多说了！
先搞清楚一个今天提到的概念：
[父视图控制器 addChildViewController:子视图控制器];
在此，图控制器A添加了另一个图控制器B，那么A充当父视图控制器，B充当子视图控制器。父视图控制器充当了视图控制器容器的角色。
addChildViewController方法：
```c++
- (void)addChildViewController:(UIViewController *)childController
```
向视图控制器容器中添加子视图控制器
childController：子视图控制器
当要添加的子视图控制器已经包含在视图控制器容器中，那么，相当于先从父视图控制器中删除，然后重新添加到父视图控制器中。
removeFromParentViewController 方法
```c++
- (void)removeFromParentViewController
```
从父视图控制器中删除。
transitionFromViewController 方法
```c++
- (void)transitionFromViewController:(UIViewController *)fromViewController
				toViewController:(UIViewController *)toViewController 
				duration:(NSTimeInterval)duration 
				options:(UIViewAnimationOptions)options 
				animations:(void (^)(void))animations 
				completion:(void (^)(BOOL finished))completion;
```
交换两个子视图控制器的位置（由于添加的顺序不同，所以子试图控制器在父视图控制器中存在层次关系）
fromViewController：当前显示的子试图控制器，将被替换为非显示状态
toViewController：将要显示的子视图控制器
duration：交换动画持续的时间，单位秒
options：动画的方式
animations：动画Block
completion：完成后执行的Block
willMoveToParentViewController 方法
```c++
- (void)willMoveToParentViewController:(UIViewController *)parent
```
当一个视图控制器从视图控制器容器中被添加或者被删除之前，该方法被调用
parent：父视图控制器，如果没有父视图控制器，将为nil
注意点：
1.当我们向我们的视图控制器容器中调用removeFromParentViewController方法时，必须要先调用该方法，且parent参数为nil：
[将要删除的视图控制器 willMoveToParentViewController:nil];
2.当我们调用addChildViewController方法时，在添加子视图控制器之前将自动调用该方法。所以，就不需要我们显示调用了。
didMoveToParentViewController 方法
```c++
- (void)didMoveToParentViewController:(UIViewController *)parent
```
当从一个视图控制容器中添加或者移除viewController后，该方法被调用。
parent：父视图控制器，如果没有父视图控制器，将为nil
当我们向我们的视图控制器容器（就是父视图控制器，它调用addChildViewController方法加入子视图控制器，它就成为了视图控制器的容器）中添加（或者删除）子视图控制器后，必须调用该方法，告诉iOS，已经完成添加（或删除）子控制器的操作。
removeFromParentViewController 方法会自动调用了该方法，所以，删除子控制器后，不需要在显示的调用该方法了。
其实，这几个方法中的API说明，看的还懂。
最后，
关于willMoveToParentViewController方法和didMoveToParentViewController方法的使用
1.这两个方法用在子试图控制器交换的时候调用！即调用transitionFromViewController 方法时，调用。
2.当调用willMoveToParentViewController方法或didMoveToParentViewController方法时，要注意他们的参数使用：
当某个子视图控制器将从父视图控制器中删除时，parent参数为nil。
即：[将被删除的子试图控制器 willMoveToParentViewController:nil];
当某个子试图控制器将加入到父视图控制器时，parent参数为父视图控制器。
即：[将被加入的子视图控制器 didMoveToParentViewController:父视图控制器];
3.无需调用[子视图控制器 willMoveToParentViewController:父视图控制器]方法。因为我们调用[父视图控制器 addChildViewController:子视图控制器]时，已经默认调用了。
只需要在transitionFromViewController方法后，调用[子视图控制器didMoveToParentViewController:父视图控制器];
4.无需调用[子视图控制器 didMoveToParentViewController:父视图控制器]方法。因为我们调用[子视图控制器 removeFromParentViewController]时，已经默认调用了。
只需要在transitionFromViewController方法之前调用：[子视图控制器 willMoveToParentViewController:nil]。