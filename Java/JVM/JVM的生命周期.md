虚拟机的启动：
Java虚拟机的启动是通过引导类加载器（bootstrap class loader）创建一个初始类（initial class） 来完成的，这个类是由虚拟机的具体实现指定的。

虚拟机退出的情况：

1. 某线程调用Runtime类或System类的exit方法，或者Runtime的halt方法，并且Java管理器也允许这次exit和halt操作。
2. 程序正常结束。
3. 程序运行过程中遇到异常或错误而异常终止。
4. 由于操作系统出现错误而导致Java虚拟机进程终止。



