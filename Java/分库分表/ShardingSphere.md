ShardingJDBC（引入依赖）

汇总设置分库分表策略

Sharding-Proxy

假装自己是一个数据库代我们管理数据库，数据库代理端口，所有的增删改查都是由Sharding-Proxy代理处理，然后操作真正的数据库。

Sharding-Sidecar

在kubernetes的云原生数据库代理，即DataBase mesh，数据网格