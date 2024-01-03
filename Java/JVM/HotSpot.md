SUN的JDK版本从1.3.1开始运用HotSpot虚拟机， 2006年底开源，主要使用C++实现，JNI接口部分用C实现。
HotSpot是较新的Java虚拟机，使用JIT(Just in Time)编译器，可以大大提高Java运行的性能。 
Java原先是把源代码编译为字节码在虚拟机执行，这样执行速度较慢。而HotSpot将常用的部分代码编译为本地(原生，native)代码，这样显着提高了性能。 
HotSpot JVM 参数可以分为规则参数(standard options)和非规则参数(non-standard options)。 规则参数相对稳定，在JDK未来的版本里不会有太大的改动。 非规则参数则有因升级JDK而改动的可能。