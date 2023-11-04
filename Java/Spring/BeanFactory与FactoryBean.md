BeanFactory：它一个基础类型的Spring IOC容器，它负责初始化各种Bean,并调用它们的生命周期方法。另外一个容器为ApplicationContext，它是Spring的一个核心容器，也是BeanFactory的一个子类，在BeanFactory的基础上增加了对国际化，资源访问，事件传播等方面的支持。

FactoryBean：用户创建Bean的一个特殊工厂Bean



参考：

[BeanFactory与FactoryBean有什么区别？_beanfactory和factorybean的区别-CSDN博客](https://blog.csdn.net/yangyin1998/article/details/131026301)