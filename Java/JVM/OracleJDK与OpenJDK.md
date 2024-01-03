Oracle JDK和Open JDK的关系：


官方的说明：
https://www.oracle.com/cn/java/technologies/javase-downloads.html
Oracle Customers and ISVs targeting Oracle LTS releases: Oracle JDK is Oracle's supported Java SE version for customers and for developing, testing, prototyping or demonstrating your Java applications.
End users and developers looking for free JDK versions: Oracle OpenJDK offers the same features and performance as Oracle JDK under the GPL license .

Oracle JDK下载路径：
https://www.oracle.com/java/technologies/javase-jdk15-downloads.html
Open JDK下载路径：
https://cn.azul.com/downloads/zulu-community/?version=java-11-lts&os=windows&architecture=x86-64-bit

Oracle与OpenJDK之间的主要区别
1. Oracle JDK版本将每三年发布一次LTS版本，而OpenJDK版本每三个月发布一次。
2. Oracle JDK将更多地关注稳定性，它重视更多的企业级用户，而OpenJDK经常发布以支持其他性能，这可能会导致不稳定。
3. Oracle JDK支持长期发布的更改，而Open JDK仅支持计划和完成下一个发行版。
4. Oracle JDK根据二进制代码许可协议获得许可，而OpenJDK根据GPL v2许可获得许可。 使用Oracle平台时会产生一些许可影响。如Oracle 宣布的那样，在没有商业许可的情况下，在2019年1月之后发布的Oracle Java SE 8的公开更新将无法用于商业，商业或生产用途。但是，OpenJDK是完全开源的，可以自由使用。
5. Oracle JDK的构建过程基于OpenJDK，因此OpenJDK与Oracle JDK之间没有技术差异。
6. 顶级公司正在使用Oracle JDK，例如Android Studio，Minecraft和IntelliJ IDEA开发工具，其中Open JDK不太受欢迎。
7. Oracle JDK具有Flight Recorder，Java Mission Control和Application Class-Data Sharing功能，Open JDK具有Font Renderer功能，这是OpenJDK与Oracle JDK之间的显着差异。
8. Oracle JDK具有良好的GC选项和更好的渲染器，而OpenJDK具有更少的GC选项，并且由于其包含自己的渲染器的分布，因此具有较慢的图形渲染器选项。
9. 在响应性和JVM性能方面，Oracle JDK与OpenJDK相比提供了更好的性能。
10. 与OpenJDK相比，Oracle JDK的开源社区较少，OpenJDK社区用户的表现优于Oracle JDK发布的功能，以提高性能。
11. 如果使用Oracle JDK会产生许可影响，而OpenJDK没有这样的问题，并且可以以任何方式使用，以满足完全开源和免费使用。
12. Oracle JDK在运行JDK时不会产生任何问题，而OpenJDK在为某些用户运行JDK时会产生一些问题。
13. 根据使用方的使用和许可协议，现有应用程序可以从Oracle JDK迁移到Open JDK，反之亦然。
14. Oracle JDK将从其10.0.X版本将收费，用户必须付费或必须依赖OpenJDK才能使用其免费版本。
15. Oracle JDK不会为即将发布的版本提供长期支持，用户每次都必须通过更新到最新版本获得支持来获取最新版本。
16. Oracle JDK以前的1.0版以前的版本是由Sun开发的，后来被Oracle收购并为其他版本维护，而OpenJDK最初只基于Java SDK或JDK版本7。
17. Oracle JDK发布时大多数功能都是开源的，其中一些功能免于开源，并且根据Sun的许可授权，而OpenJDK发布了所有功能，如开源和免费。
18. Oracle JDK完全由Oracle公司开发，而Open JDK项目由IBM，Apple，SAP AG，Redhat等顶级公司加入和合作。