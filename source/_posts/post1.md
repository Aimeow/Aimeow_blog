layout: sublime
title: Sublime Text3安装Package Control
date: 2015-05-26 10:10:03
tags:
---
按Ctrl+`调出console,然后粘贴以下代码到底部命令行并回车：
``` c++
import urllib.request,os; 
pf = 'Package Control.sublime-package';
ipp = sublime.installed_packages_path();
urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); 
open(os.path.join(ipp, pf), 'wb').write(urllib.request.urlopen( 'http://sublime.wbond.net/' + pf.replace(' ','%20')).read())
```
重启Sublime Text。 如果在Perferences->package settings中看到package control这一项，则安装成功。