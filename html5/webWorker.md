#  Web Worker
***
## 1. Web Worker 可以让你在后台运行Javascript

一般来说Javascript和页面的UI会共用一个线程，所以当点击一个按钮开始运行Javascript后，
在这段代码运行完毕之前，页面是无法响应用户操作的，换句话来说就是被“冻结”了。而这段代码可以交给Web Worker在后台运行，
那么页面在Javascript运行期间依然可以响应用户操作。后台会启动一个worker线程来执行这段代码，用户可以创建多个worker线程。
所以你可以在前台做一些小规模分布式计算之类的工作，不过Web Worker有以下一些使用限制：

* Web Worker无法访问DOM节点；
* Web Worker无法访问全局变量或是全局函数；
* Web Worker无法调用alert()或者confirm之类的函数；
* Web Worker无法访问window、document之类的浏览器全局变量；

不过Web Worker中的Javascript依然可以使用setTimeout(),setInterval()之类的函数，也可以使用XMLHttpRequest对象来做Ajax通信。




