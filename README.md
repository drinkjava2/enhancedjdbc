## EnhancedJDBC
开源协议: [Apache 2.0](http://www.apache.org/licenses/LICENSE-2.0)  

EnhancedJDBC(前身为jDbPro)是一个建立于Apache Commons DbUtils上，并对其增强了动态SQL功能的JDBC持久层工具，它是一个承上(包装JDBC，支持多种SQL写法)启下(作为ORM项目内核)的项目，但它本身也是一个独立的工具，可以单独使用，其运行环境为Java6或以上。  

作为ORM项目的内核，EnhancedJDBC仅关注于改进JDBC操作的易用性，它不考虑对象映射、关联映射、数据库方言、分布式事务等高级功能，这些高级功能属于ORM工具如jSqlBox负责的范畴。jSqlBox的设计理念是尽量将每个功能点设计成独立的小项目，隔离它们的相互依赖性，每个小项目都可以单独使用，整合在一起就成了jSqlBox，这与Hibernate之类将JDBC、ORM功能捆绑在一起的持久层工具是不同的。目前在这一理念下已经开发的工具项目有：  
1)jDialects，这是一个支持70多种方言的SQL分页、DDL支持、JPA支持工具，用于解决利用JDBC工具进行跨数据库开发的问题。  
2)jTransactions，这是一个将声明式事务作为单独的项目提供的小工具，目前包含一个微型实现TinyTx，并支持配置成使用Spring的声明式事务。  
3)jBeanBox，这是一个微型IOC/AOP工具，如果不想用笨重的Spring-Ioc,可以用它来替代。  
4)EnhancedJDBC，即本项目，主要优点是利用纯JDBC完成最主要的功能：SQL操作，但是加入了内嵌SQL式写法、分页、多租户、sharding支持，让纯JDBC开发也可以达到高效率、多功能，用最低的学习成本获得较高的开发效率和接近底层JDBC的运行效率。    
5)jSqlBox，这是一个整合了上述子项目的ORM工具，除了拥有EnhancedJDBC的所有功能并与DbUtils兼容之外，主要增加了实体映射、ActiveRecord、声明式事务、分布式事务等高级功能。得益于EnhancedJDBC等子项目做了大量底层工作，jSqlBox项目只用了约40个类就构成了一个功能完备的ORM工具。  

### 如何引入EnhancedJDBC到项目? 
在项目的pom.xml文件中加入如下行：  
```
   <dependency>  
      <groupId>com.github.drinkjava2</groupId>  
      <artifactId>enhanced-jdbc</artifactId>  
      <version>3.0.0</version> <!--或Maven最新版-->
   </dependency>
``` 
EnhancedJDBC不依赖于任何第三方库, 即可以用上述Maven的方式引入，也可以将它的源码拷到项目中即可使用。  

### 说明 
从2.0.2版本起，EnhancedJDBC即不再有自已的说明文档，因为它的功能已在jSqlBox中的用户手册中有比较详细的介绍。
以下两行是个简短的使用示例，更多使用方式请参见jSqlBox的用户手册。  
```
EnhancedJDBC jdbc= new EnhancedJDBC(someDataSource);  
jdbc.exe("update users set name=",par("Sam"), " address=", que("Canada"));
```