<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是Mybatis？

> 原文：[https://zwmst.com/1763.html](https://zwmst.com/1763.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:26:42+08:00"> 2021-08-15 </time> ](https://zwmst.com/1763.html)  1）mybatis是一个半ORM框架，它内部封装了JDBC，开发时只需要关乎sql语句本身，不需 要花费精力去处理驱动，创建连接，创建1statement等繁复过程。

2）mybatis可以使用xml或注解来配置和映射原生信息。将pijo映射成数据库中的记录，避免 了几乎所有的JDBC 代码和手动设置参数以及获取结果集。

3）通过xm文件或注解的方式将要执行的各种statement配置起来,并通java对象和statement 中sql的动态参数进行映射生成最终的sql语句,最后由mybatis框架执行sql并将结果映射java 对象返回.*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis的优缺点?

> 原文：[https://zwmst.com/1766.html](https://zwmst.com/1766.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:27:49+08:00"> 2021-08-15 </time> ](https://zwmst.com/1766.html)  Mybaits的优点：

（1）基于SQL语句编程，相当灵活，不会对应用程序或者数据库的现有设计造成任何影响， SQL写在XML里，解除sql与程序代码的耦合，便于统一管理；提供XML标签，支持编写动态 SQL语句，并可重用。

（2）与JDBC相比，减少了50%以上的代码量，消除了JDBC大量冗余的代码，不需要手动开关连接；

（3）很好的与各种数据库兼容（因为MyBatis使用JDBC来连接数据库，所以只要JDBC支持的 数据库MyBatis都支持）。

（4）能够与Spring很好的集成；

（5）提供映射标签，支持对象与数据库的ORM字段关系映射；提供对象关系映射标签，支持对象关系组件维护。

MyBatis框架的缺点：

（1）SQL语句的编写工作量较大，尤其当字段多、关联表多时，对开发人员编写SQL语句的功 底有一定要求。

（2）SQL语句依赖于数据库，导致数据库移植性差，不能随意更换数据库。

MyBatis框架适用场合：

（1）MyBatis专注于SQL本身，是一个足够灵活的DAO层解决方案。

（2）对性能的要求很高，或者需求变化较多的项目，如互联网项目，MyBatis将是不错的选 择。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis使用场合?

> 原文：[https://zwmst.com/1768.html](https://zwmst.com/1768.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:28:07+08:00"> 2021-08-15 </time> ](https://zwmst.com/1768.html)  专注于sql本身,是一个足够灵活的dao层解决方案.,对性能的要求很高,或者需求多变的项目*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# #{}和${}的区别是什么？

> 原文：[https://zwmst.com/1771.html](https://zwmst.com/1771.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:28:36+08:00"> 2021-08-15 </time> ](https://zwmst.com/1771.html)  # {}是预编译处理，${}是字符串替换。

Mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋 值；

Mybatis在处理{}时，就是把时，就是把{}替换成变量的值。

使用#{}可以有效的防止SQL注入，提高系统安全性。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 当实体类的属性名和表种字段名不一致怎么办?

> 原文：[https://zwmst.com/1773.html](https://zwmst.com/1773.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:28:54+08:00"> 2021-08-15 </time> ](https://zwmst.com/1773.html)  有两种解决方案:可以在sql语句给字段名取别名,别名于实体类属性名同名,也可以用resultMap 来映射字段名和实体类属性名一一对应*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis是如何将sql执行结果封装为目标对象并返回的？都有哪些映射形式？

> 原文：[https://zwmst.com/1775.html](https://zwmst.com/1775.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:29:10+08:00"> 2021-08-15 </time> ](https://zwmst.com/1775.html)  第一种是使用resultMap标签，逐一定义数据库列名和对象属性名之间的映射关系。

第二种是使用sql列的别名功能，将列的别名书写为对象属性名。

有了列名与属性名的映射关系后，Mybatis通过反射创建对象，同时使用反射给对象的属性逐 一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何获取自动生成的(主)键值?

> 原文：[https://zwmst.com/1777.html](https://zwmst.com/1777.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:29:24+08:00"> 2021-08-15 </time> ](https://zwmst.com/1777.html)  ```
<insert id=”insertname” usegeneratedkeys=”true” keyproperty=”id”>
        insert into names (name) values (#{name}) 
</insert>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？

> 原文：[https://zwmst.com/1779.html](https://zwmst.com/1779.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:29:34+08:00"> 2021-08-15 </time> ](https://zwmst.com/1779.html)  不同的Xml映射文件，如果配置了namespace，那么id可以重复；如果没有配置 namespace，那么id不能重复*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis动态SQL？

> 原文：[https://zwmst.com/1781.html](https://zwmst.com/1781.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:29:44+08:00"> 2021-08-15 </time> ](https://zwmst.com/1781.html)  1) 传统的JDBC的方法，在组合SQL语句的时候需要去拼接，稍微不注意就会少少了一个空 格，标点符号，都会导致系统错误。Mybatis的动态SQL就是为了解决这种问题而产生的； Mybatis的动态SQL语句值基于OGNL表达式的，方便在SQL语句中实现某些逻辑；可以使用 标签组合成灵活的sql语句，提供开发的效率。

2) Mybatis的动态SQL标签主要由以下几类： If语句（简单的条件判断） Choose(when/otherwise),相当于java语言中的switch，与jstl中choose类似 Trim(对包含 的内容加上prefix，或者suffix) Where(主要是用来简化SQL语句中where条件判断，能智能 的处理and/or 不用担心多余的语法导致的错误) Set(主要用于更新时候) Foreach(一般使用在 mybatis in语句查询时特别有用)*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 说一下resultMap和resultType？

> 原文：[https://zwmst.com/1783.html](https://zwmst.com/1783.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:29:56+08:00"> 2021-08-15 </time> ](https://zwmst.com/1783.html)  resultmap是手动提交，人为提交，resulttype是自动提交 MyBatis中在查询进行select映射的时候，返回类型可以用resultType，也可以用 resultMap，resultType是直接表示返回类型的，而resultMap则是对外部ResultMap的引 用，但是resultType跟resultMap不能同时存在。

在MyBatis进行查询映射时，其实查询出来的每一个属性都是放在一个对应的Map里面的，其 中键是属性名，值则是其对应的值。

1.当提供的返回类型属性是resultType时，MyBatis会将Map里面的键值对取出赋给resultType所指定的对象对应的属性。所以其实MyBatis的每一个查询映射的返回类型都是 ResultMap，只是当提供的返回类型属性是resultType的时候，MyBatis对自动的给把对应 的值赋给resultType所指定对象的属性。

2.当提供的返回类型是resultMap时，因为Map不能很好表示领域模型，就需要自己再进一步 的把它转化为对应的对象，这常常在复杂查询中很有作用。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis全局配置文件中有哪些标签?分别代表什么意思?

> 原文：[https://zwmst.com/1785.html](https://zwmst.com/1785.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:30:11+08:00"> 2021-08-15 </time> ](https://zwmst.com/1785.html)  configuration 配置

properties 属性:可以加载properties配置文件的信息

settings 设置：可以设置mybatis的全局属性

typeAliases 类型命名

typeHandlers 类型处理器

objectFactory 对象工厂

plugins 插件

environments 环境

environment 环境变量

transactionManager 事务管理器

dataSource 数据源

mappers 映射器*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis能执行一对一、一对多的关联查询吗？都有哪些实现方式，以及它们之间的区别。

> 原文：[https://zwmst.com/1787.html](https://zwmst.com/1787.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:30:21+08:00"> 2021-08-15 </time> ](https://zwmst.com/1787.html)  答：能，Mybatis不仅可以执行一对一、一对多的关联查询，还可以执行多对一，多对多的关 联查询，多对一查询，其实就是一对一查询，只需要把selectOne()修改为selectList()即可； 多对多查询，其实就是一对多查询，只需要把selectOne()修改为selectList()即可。

关联对象查询，有两种实现方式，一种是单独发送一个sql去查询关联对象，赋给主对象， 然后返回主对象。另一种是使用嵌套查询，嵌套查询的含义为使用join查询，一部分列是A对 象的属性值，另外一部分列是关联对象B的属性值，好处是只发一个sql查询，就可以把主对象 和其关联对象查出来。

那么问题来了，join查询出来100条记录，如何确定主对象是5个，而不是100个？其去重 复的原理是 resultMap标签内的 id 子标签，指定了唯一确定一条记录的id列，Mybatis根据 id 列值来完成100条记录的去重复功能， id 可以有多个，代表了联合主键的语意。

同样主对象的关联对象，也是根据这个原理去重复的，尽管一般情况下，只有主对象会有 重复记录，关联对象一般不会重复。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis是否支持延迟加载？如果支持，它的实现原理是什么？

> 原文：[https://zwmst.com/1789.html](https://zwmst.com/1789.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:30:32+08:00"> 2021-08-15 </time> ](https://zwmst.com/1789.html)  Mybatis仅支持association关联对象和collection关联集合对象的延迟加载，association指 的就是一对一，collection指的就是一对多查询。在Mybatis配置文件中，可以配置是否启用 延迟加载lazyLoadingEnabled=true|false。

它的原理是，使用CGLIB创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比 如调用a.getB().getName()，拦截器invoke()方法发现a.getB()是null值，那么就会单独发送 事先保存好的查询关联B对象的sql，把B查询上来，然后调用a.setB(b)，于是a的对象b属性就 有值了，接着完成a.getB().getName()方法的调用。这就是延迟加载的基本原理。

当然了，不光是Mybatis，几乎所有的包括Hibernate，支持延迟加载的原理都是一样的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis都有哪些Executor执行器？它们之间的区别是什么？

> 原文：[https://zwmst.com/1791.html](https://zwmst.com/1791.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:30:43+08:00"> 2021-08-15 </time> ](https://zwmst.com/1791.html)  Mybatis有三种基本的Executor执行器，SimpleExecutor、ReuseExecutor、 BatchExecutor。

SimpleExecutor：每执行一次update或select，就开启一个Statement对象，用完立刻关闭 Statement对象。

ReuseExecutor：执行update或select，以sql作为key查找Statement对象，存在就使用， 不存在就创建，用完后，不关闭Statement对象，而是放置于Map<String, Statement>内， 供下一次使用。简言之，就是重复使用Statement对象。

BatchExecutor：执行update（没有select，JDBC批处理不支持select），将所有sql都添加 到批处理中（addBatch()），等待统一执行（executeBatch()），它缓存了多个Statement 对象，每个Statement对象都是addBatch()完毕后，等待逐一执行executeBatch()批处理。 与JDBC批处理相同。

作用范围：Executor的这些特点，都严格限制在SqlSession生命周期范围内。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis的一级、二级缓存

> 原文：[https://zwmst.com/1793.html](https://zwmst.com/1793.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-15T16:30:53+08:00"> 2021-08-15 </time> ](https://zwmst.com/1793.html)  （1）一级缓存: 基于 PerpetualCache 的 HashMap 本地缓存，其存储作用域为 Session，当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认打开一级缓存。

（2）二级缓存与一级缓存其机制相同，默认也是采用 PerpetualCache，HashMap 存储，不 同在于其存储作用域为 Mapper(Namespace)，并且可自定义存储源，如 Ehcache。默认不 打开二级缓存，要开启二级缓存，使用二级缓存属性类需要实现Serializable序列化接口(可用 来保存对象的状态),可在它的映射文件中配置 ；

（3）对于缓存数据更新机制，当某一个作用域(一级缓存 Session/二级缓存Namespaces)的 进行了C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear 掉并重新更新，如果开 启了二级缓存，则只根据配置判断是否刷新。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是 Mybatis？

> 原文：[https://zwmst.com/2242.html](https://zwmst.com/2242.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:55:40+08:00"> 2021-08-21 </time> ](https://zwmst.com/2242.html)  *   （1） Mybatis 是一个半 ORM（对象关系映射）框架，它内部封装了 JDBC，开发时只需要关注 SQL 语句本身，不需要花费精力去处理加载驱动、创建连接、创建 statement 等繁杂的过程。程序员直接编写原生态 sql，可以严格控制 sql 执行性能，灵活度高。
*   （2） MyBatis 可以使用 XML 或注解来配置和映射原生信息，将 POJO 映射成数据库中的记录，避免了几乎所有的 JDBC 代码和手动设置参数以及获取结果集。
*   （3） 通过 xml 文件或注解的方式将要执行的各种 statement 配置起来，并通过 java 对象和 statement 中 sql 的动态参数进行映射生成最终执行的 sql 语句，最后由 mybatis 框架执行 sql 并将结果映射为 java 对象并返回。（从执行 sql 到返回 result 的过程）。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybaits 的优点：

> 原文：[https://zwmst.com/2244.html](https://zwmst.com/2244.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:55:56+08:00"> 2021-08-21 </time> ](https://zwmst.com/2244.html)  *   （1） 基 于 SQL 语句编程，相当灵活，不会对应用程序或者数据库的现有设计造成任何影响，SQL 写在 XML 里，解除 sql 与程序代码的耦合，便于统一管理；提供 XML 标签，支持编写动态 SQL 语句，并可重用。
*   （2） 与 JDBC 相比，减少了 50%以上的代码量，消除了 JDBC 大量冗余的代码，不需要手动开关连接；
*   （3） 很好的与各种数据库兼容（因为 MyBatis 使用 JDBC 来连接数据库，所以只要 JDBC 支持的数据库 MyBatis 都支持）。
*   （4） 能够与 Spring 很好的集成；
*   （5） 提供映射标签，支持对象与数据库的 ORM 字段关系映射；提供对象关系映射标签，支持对象关系组件维护。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# MyBatis 框架的缺点：

> 原文：[https://zwmst.com/2246.html](https://zwmst.com/2246.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:56:07+08:00"> 2021-08-21 </time> ](https://zwmst.com/2246.html)  *   （1） SQL 语句的编写工作量较大，尤其当字段多、关联表多时，对开发人员编写 SQL 语句的功底有一定要求。
*   （2） SQL 语句依赖于数据库，导致数据库移植性差，不能随意更换数据库。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# MyBatis 框架适用场合：

> 原文：[https://zwmst.com/2248.html](https://zwmst.com/2248.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:56:18+08:00"> 2021-08-21 </time> ](https://zwmst.com/2248.html)  *   （1） MyBatis 专注于 SQL 本身，是一个足够灵活的 DAO 层解决方案。
*   （2） 对性能的要求很高，或者需求变化较多的项目，如互联网项目，MyBatis 将是不错的选择。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# MyBatis 与 Hibernate 有哪些不同？

> 原文：[https://zwmst.com/2250.html](https://zwmst.com/2250.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:56:33+08:00"> 2021-08-21 </time> ](https://zwmst.com/2250.html)  *   （1） Mybatis 和 hibernate 不同，它不完全是一个 ORM 框架，因为 MyBatis 需要程序员自己编写 Sql 语句。
*   （2） Mybatis 直接编写原生态 sql，可以严格控制 sql 执行性能，灵活度 高，非常适合对关系数据模型要求不高的软件开发，因为这类软件需求变化频繁，一但需求变化要求迅速输出成果。但是灵活的前提是 mybatis 无法做到数据库无关性，如果需要实现支持多种数据库的软件，则需要自定义多套 sql 映射文件，工作量大。
*   （3） Hibernate 对象/关系映射能力强，数据库无关性好，对于关系模型要求高的软件，如果用 hibernate 开发可以节省很多代码，提高效率*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# #{}和${}的区别是什么？

> 原文：[https://zwmst.com/2252.html](https://zwmst.com/2252.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:56:56+08:00"> 2021-08-21 </time> ](https://zwmst.com/2252.html)  **#{}是预编译处理，${}是字符串替换。**

Mybatis 在处理#{}时，会将 sql 中的#{}替换为?号，调用PreparedStatement 的 set 方法来赋值；
Mybatis 在处理${}时，就是把${}替换成变量的值。使用#{}可以有效的防止 SQL 注入，提高系统安全性。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 当实体类中的属性名和表中的字段名不一样 ，怎么办 ？

> 原文：[https://zwmst.com/2254.html](https://zwmst.com/2254.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:57:10+08:00"> 2021-08-21 </time> ](https://zwmst.com/2254.html)  *   第 1 种： 通过在查询的 sql 语句中定义字段名的别名，让字段名的别名和实体类的属性名一致。

```
<select id=”selectorder” parametertype=”int” resultetype=” me.gacl.domain.order”>
select order_id id, order_no orderno ,order_price price form orders where order_id=#{id};
</select>
```

*   第 2 种： 通过 $< resultMap >$ 来映射字段名和实体类属性名的一一对应的关系。

```
<select id="getOrder" parameterType="int" resultMap="orderresultmap">
select * from orders where order_id=#{id}
</select>
<resultMap type=”me.gacl.domain.order” id=”orderresultmap”>
<!–用 id 属性来映射主键字段–>
<id property=”id” column=”order_id”>
<!–用 result 属性来映射非主键字段，property 为实体类属性名，column 为数据表中的属性–>
<result property = “orderno” column =”order_no”/>
<result property=”price” column=”order_price” />
</reslutMap>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 模糊查询 like 语句该怎么写

> 原文：[https://zwmst.com/2256.html](https://zwmst.com/2256.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:57:26+08:00"> 2021-08-21 </time> ](https://zwmst.com/2256.html)  *   第 1 种：在 Java 代码中添加 sql 通配符。

    ```
    string wildcardname = “%smi%”; 
    list<name> names = mapper.selectlike(wildcardname); 
    <select id=”selectlike”> 
    select * from foo where bar like #{value} 
    </select>
    ```

*   第 2 种：在 sql 语句中拼接通配符，会引起 sql 注入

    ```
    string wildcardname = “smi”; list<name> names = mapper.selectlike(wildcardname); 
    <select id=”selectlike”> 
    select * from foo where bar like "%"#{value}"%" 
    </select>
    ```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 通常一个 Xml 映射文件，都会写一个 Dao 接口与之对应，请问，这个 Dao 接口的工作原理是什么？Dao 接口里的方法，参数不同时，方法能重载吗？

> 原文：[https://zwmst.com/2258.html](https://zwmst.com/2258.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:57:38+08:00"> 2021-08-21 </time> ](https://zwmst.com/2258.html)  **Dao 接口即 Mapper 接口。**

*   接口的全限名，就是映射文件中的 namespace 的值；
*   接口的方法名，就是映射文件中 Mapper 的 Statement 的 id 值；
*   接口方法内的参数，就是传递给 sql 的参数。
    Mapper 接口是没有实现类的，当调用接口方法时，接口全限名+方法名拼接字符串作为 key 值，可唯一定位一个 MapperStatement。
    在 Mybatis 中，每一个 $<$select$>$、$<$insert$>$、$<$update$>$、$<$delete$>$标签，都会被解析为一个 MapperStatement 对象。
    举例：com.mybatis3.mappers.StudentDao.findStudentById，可以唯一找到 namespace 为 com.mybatis3.mappers.StudentDao 下面 id 为 findStudentById 的 MapperStatement。

Mapper 接口里的方法，是不能重载的，因为是使用 全限名+方法名 的保存和寻找策略。
Mapper 接口的工作原理是 JDK 动态代理，Mybatis 运行时会使用 JDK 动态代理为 Mapper 接口生成代理对象 proxy，代理对象会拦截接口方法，转而执行 MapperStatement 所代表的 sql，然后将 sql 执行结果返回。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis 是如何进行分页的？分页插件的原理是什么？

> 原文：[https://zwmst.com/2260.html](https://zwmst.com/2260.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:57:50+08:00"> 2021-08-21 </time> ](https://zwmst.com/2260.html)  Mybatis 使用 RowBounds 对象进行分页，它是针对 ResultSet 结果集执行的内存分页，而非物理分页。可以在 sql 内直接书写带有物理分页的参数来完成物理分页功能，也可以使用分页插件来完成物理分页。
分页插件的基本原理是使用 Mybatis 提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的 sql，然后重写 sql，根 据 dialect 方言，添加对应的物理分页语句和物理分页参数。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis 是如何将 sql 执行结果封装为目标对象并返回的？都有哪些映射形式？

> 原文：[https://zwmst.com/2262.html](https://zwmst.com/2262.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:58:01+08:00"> 2021-08-21 </time> ](https://zwmst.com/2262.html)  *   第一种是使用$<$resultMap$>$标签，逐一定义数据库列名和对象属性名之间的映射关系。
*   二种是使用 sql 列的别名功能，将列的别名书写为对象属性名。
    有了列名与属性名的映射关系后，Mybatis 通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何执行批量插入

> 原文：[https://zwmst.com/2264.html](https://zwmst.com/2264.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:58:13+08:00"> 2021-08-21 </time> ](https://zwmst.com/2264.html)  *   首先,创建一个简单的 insert 语句:

    ```
    <insert id=”insertname”> insert into names (name) values (#{ value
    }
    )
    </insert> 
    ```

*   然后在 java 代码中像下面这样执行批处理插入:

    ```
    list < string > names = new arraylist();
    names.add(“fred”); names.add(“barney”); names.add(“betty”); names.add(“wilma”); // 注意这里 executortype.batch sqlsession sqlsession = sqlsessionfactory.opensession(executortype.batch); try { namemapper mapper = sqlsession.getmapper(namemapper.class); for (string name: names) { mapper.insertname(name);
    }
    sqlsession.commit();
    }
    catch (Exception e) {
    e.printStackTrace(); sqlSession.rollback(); throw e;
    } finally { sqlsession.close(); }
    ```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 如何获取自动生成的(主)键值

> 原文：[https://zwmst.com/2266.html](https://zwmst.com/2266.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-21T11:58:29+08:00"> 2021-08-21 </time> ](https://zwmst.com/2266.html)  insert 方法总是返回一个 int 值 ，这个值代表的是插入的行数。
如果采用自增长策略，自动生成的键值在 insert 方法执行完后可以被设置到传入的参数对象中。
示例：

```
<insert id=”insertname” usegeneratedkeys=”true” keyproperty=” id”>
insert into names (name) values (#{ name
}
)
</insert> name name = new name(); name.setname(“fred”);
int rows = mapper.insertname(name);
// 完成后,id 已经被设置到对象中
system.out.println(“rows inserted = ” + rows);
system.out.println(“generated key value = ” + name.getid());
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 在 mapper 中如何传递多个参数

> 原文：[https://zwmst.com/2270.html](https://zwmst.com/2270.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:31:59+08:00"> 2021-08-22 </time> ](https://zwmst.com/2270.html)  *   第一种：DAO 层的函数public UserselectUser(String name,String area);对应的 xml,#{0}代表接收的是 dao 层中的第一个参数，#{1}代表 dao 层中第二参数，更多参数一致往后加即可。

    ```
    <select id="selectUser"resultMap="BaseResultMap"> select \* fromuser_user_t whereuser_name = #{0} anduser_area=#{1} </select>
    ```

*   第二种： 使用 @param 注解:

    ```
    public interface usermapper { user selectuser(@param(“username”) string
    username,@param(“hashedpassword”) string hashedpassword);
    }
    ```

    然后,就可以在 xml 像下面这样使用(推荐封装为一个 map,作为单个参数传递给 mapper):

    ```
    <select id=”selectuser” resulttype=”user”>
    select id, username, hashedpassword from some_table
    where username = #{username} and hashedpassword = #{hashedpassword}
    </select>
    ```

*   第三种：多个参数封装成 map

    ```
    try {
    //映射文件的命名空间.SQL 片段的 ID，就可以调用对应的映射文件中的
    SQL
    //由于我们的参数超过了两个，而方法中只有一个 Object 参数收集，因此我们使用 Map 集合来装载我们的参数
    Map < String, Object > map = new HashMap(); map.put("start", start); map.put("end", end);
    return sqlSession.selectList("StudentID.pagination", map);
    }
    catch (Exception e) {
    e.printStackTrace(); sqlSession.rollback(); throw e;
    } finally {
    MybatisUtil.closeSqlSession();
    }
    ```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis 动态 sql 有什么用？执行原理？有哪些动态 sql？

> 原文：[https://zwmst.com/2272.html](https://zwmst.com/2272.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:32:22+08:00"> 2021-08-22 </time> ](https://zwmst.com/2272.html)  Mybatis 动态 sql 可以在 Xml 映射文件内，以标签的形式编写动态 sql，执行原理是根据表达式的值 完成逻辑判断并动态拼接 sql 的功能。
Mybatis 提供了 9 种动态 sql 标签：
**trim | where | set | foreach | if | choose| when | otherwise | bind。***
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Xml 映射文件中，除了常见的标签之外，还有哪些标签？

> 原文：[https://zwmst.com/2274.html](https://zwmst.com/2274.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:32:34+08:00"> 2021-08-22 </time> ](https://zwmst.com/2274.html)  答：$<$resultMap$>$、$<$parameterMap$>$、$<$sql$>$、$<$include$>$、$<$selectKey$>4，加上动态 sql 的 9 个标签，其中$<$sql$>$为 sql 片段标签，通过$<$include$>$标签引入 sql 片段，$<$selectKey$>为不支持自增的主键生成策略标签。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis 的 Xml 映射文件中，不同的 Xml 映射文件，id 是否可以重复？

> 原文：[https://zwmst.com/2276.html](https://zwmst.com/2276.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:32:46+08:00"> 2021-08-22 </time> ](https://zwmst.com/2276.html)  不同的 Xml 映射文件，如果配置了 namespace，那么 id 可以重复；如果没有配置 namespace，那么 id 不能重复；
原因就是 namespace+id 是作为 Map$<$String, MapperStatement$>$的 key 使用的，如果没有 namespace，就剩下 id，那么，id 重复会导致数据互相覆盖。
有了 namespace，自然 id 就可以重复，namespace 不同，namespace+id 自然也就不同。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 为什么说 Mybatis 是半自动 ORM 映射工具？它与全自动的区别在哪里？

> 原文：[https://zwmst.com/2278.html](https://zwmst.com/2278.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:36:45+08:00"> 2021-08-22 </time> ](https://zwmst.com/2278.html)  Hibernate 属于全自动 ORM 映射工具，使用 Hibernate 查询关联对象或者关联集合对象时，可以根据对象关系模型直接获取，所以它是全自动的。
而Mybatis 在查询关联对象或关联集合对象时，需要手动编写 sql 来完成，所以，称之为半自动 ORM 映射工具。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 一对一、一对多的关联查询 ？

> 原文：[https://zwmst.com/2280.html](https://zwmst.com/2280.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:36:58+08:00"> 2021-08-22 </time> ](https://zwmst.com/2280.html)  ```
<mapper namespace="com.lcb.mapping.userMapper"> 
<!--association 一对一关联查询 --> 
<select id="getClass" parameterType="int" resultMap="ClassesResultMap"> select * from class c,teacher t where c.teacher_id=t.t_id and 
c.c_id=#{id} </select> 
<resultMap type="com.lcb.user.Classes" id="ClassesResultMap"> 
<!-- 实体类的字段名和数据表的字段名映射 --> 
<id property="id" column="c_id"/> 
<result property="name" column="c_name"/> 
<association property="teacher" javaType="com.lcb.user.Teacher"> <id property="id" column="t_id"/> 
<result property="name" column="t_name"/> 
</association> 
</resultMap> 
<!--collection 一对多关联查询 --> 
<select id="getClass2" parameterType="int" resultMap="ClassesResultMap2"> 
select * from class c,teacher t,student s where c.teacher_id=t.t_id and c.c_id=s.class_id and c.c_id=#{id} 
</select> 
<resultMap type="com.lcb.user.Classes" id="ClassesResultMap2"> 
<id property="id" column="c_id"/> 
<result property="name" column="c_name"/> 
<association property="teacher" javaType="com.lcb.user.Teacher"> <id property="id" column="t_id"/> 
<result property="name" column="t_name"/> 
</association> 
<collection property="student" ofType="com.lcb.user.Student"> <id property="id" column="s_id"/> 
<result property="name" column="s_name"/> 
</collection> 
</resultMap> 
</mapper>
```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# MyBatis 实现一对一有几种方式

> 原文：[https://zwmst.com/2282.html](https://zwmst.com/2282.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:37:08+08:00"> 2021-08-22 </time> ](https://zwmst.com/2282.html)  有**联合查询**和**嵌套查询**。
联合查询是几个表联合查询,只查询一次, 通过在resultMap 里面配置 association 节点配置一对一的类就可以完成；
嵌套查询是先查一个表，根据这个表里面的结果的 外键 id，去再另外一个表里面查询数据,也是通过 association 配置，但另外一个表的查询通过 select 属性配置。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# MyBatis 实现一对多有几种方式,怎么操作的？

> 原文：[https://zwmst.com/2284.html](https://zwmst.com/2284.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:37:19+08:00"> 2021-08-22 </time> ](https://zwmst.com/2284.html)  有**联合查询**和**嵌套查询**。
联合查询是几个表联合查询,只查询一次,通过在resultMap 里面的 collection 节点配置一对多的类就可以完成；
嵌套查询是先查一个表,根据这个表里面的 结果的外键 id,去再另外一个表里面查询数据, 也是通过配置 collection,但另外一个表的查询通过 select 节点配置。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis 是否支持延迟加载？如果支持，它的实现原理是什么？

> 原文：[https://zwmst.com/2286.html](https://zwmst.com/2286.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:37:30+08:00"> 2021-08-22 </time> ](https://zwmst.com/2286.html)  答：Mybatis 仅支持 association 关联对象和 collection 关联集合对象的延迟加载，**association 指的就是一对一，collection 指的就是一对多查询**。
在 Mybatis 配置文件中，可以配置是否启用延迟加载 lazyLoadingEnabled=true|false。
**它的原理是**，使用 CGLIB 创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比如调用 a.getB().getName()，拦截器 invoke()方法发现a.getB()是 null 值，那么就会单独发送事先保存好的查询关联 B 对象的 sql，把 B 查询上来，然后调用 a.setB(b)，于是 a 的对象 b 属性就有值了，接着完成 a.getB().getName()方法的调用。
这就是延迟加载的基本原理。当然了，不光是 Mybatis，几乎所有的包括 Hibernate，支持延迟加载的原理都是一样的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 什么是 MyBatis 的接口绑定？有哪些实现方式？

> 原文：[https://zwmst.com/2288.html](https://zwmst.com/2288.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:37:45+08:00"> 2021-08-22 </time> ](https://zwmst.com/2288.html)  **接口绑定**，就是在 MyBatis 中任意定义接口,然后把接口里面的方法和 SQL 语句绑定, 我们直接调用接口方法就可以,这样比起原来了 SqlSession 提供的方法我们可以有更加灵活的选择和设置。
接口绑定有两种实现方式:

*   一种是通过注解绑定，就是在接口的方法上面加上 @Select、@Update 等注解，里面包含 Sql 语句来绑定；
*   另外一种就是通过 xml 里面写 SQL 来绑定, 在这种情况下,要指定 xml 映射文件里面的 namespace 必须为接口的全路径名。当 Sql 语句比较简单时候,用注解绑定, 当 SQL 语句比较复杂时候,用 xml 绑定,一般用 xml 绑定的比较多。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mybatis 的一级、二级缓存

> 原文：[https://zwmst.com/2290.html](https://zwmst.com/2290.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:37:58+08:00"> 2021-08-22 </time> ](https://zwmst.com/2290.html)  *   1） 一级缓存: 基于 PerpetualCache 的 HashMap 本地缓存，其存储作用域为Session，当 Session flush 或 close 之后，该 Session 中的所有 Cache 就将清空，默认打开一级缓存。
*   2） 二级缓存与一级缓存其机制相同，默认也是采用 PerpetualCache，HashMap 存储，不同在于其存储作用域为 Mapper(Namespace)，并且可自定义存储源，如 Ehcache。默认不打开二级缓存，要开启二级缓存，使用二级缓存属性类需要实现 Serializable 序列化接口(可用来保存对象的状态),可在它的映射文件中配置 <cache>；</cache>
*   3） 对于缓存数据更新机制，当某一个作用域(一级缓存 Session/二级缓存Namespaces)的进行了 C/U/D 操作后，默认该作用域下所有 select 中的缓存将被 clear。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 使用 MyBatis 的 mapper 接口调用时有哪些要求？

> 原文：[https://zwmst.com/2292.html](https://zwmst.com/2292.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:38:09+08:00"> 2021-08-22 </time> ](https://zwmst.com/2292.html)  *   （1） Mapper 接口方法名和 mapper.xml 中定义的每个 sql 的 id 相同；
*   （2） Mapper 接口方法的输入参数类型和 mapper.xml 中定义的每个 sql 的 parameterType 的类型相同；
*   （3） Mapper 接口方法的输出参数类型和 mapper.xml 中定义的每个 sql 的 resultType 的类型相同；
*   （4） Mapper.xml 文件中的 namespace 即是 mapper 接口的类路径。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# Mapper 编写有哪几种方式？

> 原文：[https://zwmst.com/2294.html](https://zwmst.com/2294.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:38:19+08:00"> 2021-08-22 </time> ](https://zwmst.com/2294.html)  ## 第一种：接口实现类继承 SqlSessionDaoSupport：

使用此种方法需要编写 mapper 接口，mapper 接口实现类、mapper.xml 文件。

*   （1） 在 sqlMapConfig.xml 中配置 mapper.xml 的位置

    ```
    <mappers> 
    <mapper resource="mapper.xml 文件的地址" /> 
    <mapper resource="mapper.xml 文件的地址" /> 
    </mappers>
    ```

*   （2） 定义 mapper 接口
*   （3） 实现类集成 SqlSessionDaoSupport mapper 方法中可以 this.getSqlSession()进行数据增删改查。
*   （4） spring 配置

    ```
    <bean id=" " class="mapper 接口的实现"> <property name="sqlSessionFactory" 
    ref="sqlSessionFactory"></property> 
    </bean>
    ```

    ## 第二种：使用 org.mybatis.spring.mapper.MapperFactoryBean：

*   （1） 在 sqlMapConfig.xml 中配置 mapper.xml 的位置，如果 mapper.xml 和mappre 接口的名称相同且在同一个目录，这里可以不用配置

    ```
    <mappers> 
    <mapper resource="mapper.xml 文件的地址" /> 
    <mapper resource="mapper.xml 文件的地址" /> 
    </mappers>
    ```

*   （2） 定义 mapper 接口：
*   （3） mapper.xml 中的 namespace 为 mapper 接口的地址
*   （4） mapper 接口中的方法名和 mapper.xml 中的定义的 statement 的 id 保持一致
*   （5） Spring 中定义

    ```
    <bean id="" class="org.mybatis.spring.mapper.MapperFactoryBean"> 
    <property name="mapperInterface" value="mapper 接口地址" /> 
    <property name="sqlSessionFactory" ref="sqlSessionFactory" /> 
    </bean>
    ```

    ## 第三种：使用 mapper 扫描器：

*   （1） mapper.xml 文件编写：
    mapper.xml 中的 namespace 为 mapper 接口的地址； mapper 接口中的方法名和 mapper.xml 中的定义的 statement 的 id 保持一致；
    如果将 mapper.xml 和 mapper 接口的名称保持一致则不用在 sqlMapConfig.xml 中进行配置。
*   （2） 定义 mapper 接口：
    注意 mapper.xml 的文件名和 mapper 的接口名称保持一致，且放在同一个目录
*   （3） 配置 mapper 扫描器：

    ```
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer"> 
    <property name="basePackage" value="mapper 接口包地址 
    "></property> 
    <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"/> 
    </bean>
    ```

*   （4） 使用扫描器后从 spring 容器中获取 mapper 的实现对象。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 简述 Mybatis 的插件运行原理，以及如何编写一个插件。

> 原文：[https://zwmst.com/2296.html](https://zwmst.com/2296.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-08-22T11:38:30+08:00"> 2021-08-22 </time> ](https://zwmst.com/2296.html)  答：Mybatis 仅可以编写针对 **ParameterHandler、ResultSetHandler、 StatementHandler、Executor** 这 4 种接口的插件，Mybatis 使用 JDK 的动态代理，为需要拦截的接口生成代理对象以实现接口方法拦截功能，每当执行这 4 种接口对象的方法时，就会进入拦截方法，具体就是 InvocationHandler 的 invoke()方法，当然，只会拦截那些你指定需要拦截的方法。
**编写插件**：实现 Mybatis 的 Interceptor 接口并复写 intercept()方法，然后在给插件编写注解，指定要拦截哪一个接口的哪些方法即可，记住，别忘了在配置文件中配置你编写的插件。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 269.Mybatis 缓存

> 原文：[https://zwmst.com/3526.html](https://zwmst.com/3526.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-09-19T21:01:10+08:00"> 2021-09-19 </time> ](https://zwmst.com/3526.html)  Mybatis 中有一级缓存和二级缓存，默认情况下一级缓存是开启的，而且是不能关闭的。一级缓存是指 SqlSession 级别的缓存，当在同一个 SqlSession 中进行相同的 SQL 语句查询时，第二次以后的查询不会从数据库查询，而是直接从缓存中获取，一级缓存最多缓存 1024 条 SQL。二级缓存是指可以跨 SqlSession 的缓存。是 mapper 级别的缓存，对于 mapper 级别的缓存不同的sqlsession 是可以共享的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 270.Mybatis 的一级缓存原理（sqlsession 级别）

> 原文：[https://zwmst.com/3528.html](https://zwmst.com/3528.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-09-19T21:02:42+08:00"> 2021-09-19 </time> ](https://zwmst.com/3528.html)  第一次发出一个查询 sql，sql 查询结果写入 sqlsession 的一级缓存中，缓存使用的数据结构是一个 map。

**key：MapperID+offset+limit+Sql+所有的入参**

value：用户信息

同一个 sqlsession 再次发出相同的 sql，就从缓存中取出数据。**如果两次中间出现 commit 操作（修改、添加、删除），本 sqlsession 中的一级缓存区域全部清空，下次再去缓存中查询不到所以要从数据库查询**，从数据库查询到再写入缓存。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 271.二级缓存原理（mapper 基本）

> 原文：[https://zwmst.com/3530.html](https://zwmst.com/3530.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-09-19T21:04:09+08:00"> 2021-09-19 </time> ](https://zwmst.com/3530.html)  二级缓存的范围是 mapper 级别（mapper 同一个命名空间），mapper 以命名空间为单位创建缓存数据结构，结构是 map。mybatis 的二级缓存是通过 CacheExecutor 实现的。CacheExecutor其实是 Executor 的代理对象。所有的查询操作，在 CacheExecutor 中都会先匹配缓存中是否存在，不存在则查询数据库。

key：MapperID+offset+limit+Sql+所有的入参

**具体使用需要配置**：

1.  Mybatis 全局配置中启用二级缓存配置
2.  在对应的 Mapper.xml 中配置 cache 节点
3.  在对应的 select 查询节点中添加 useCache=true*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1084.什么是 MyBatis？

> 原文：[https://zwmst.com/5460.html](https://zwmst.com/5460.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:21:02+08:00"> 2021-10-25 </time> ](https://zwmst.com/5460.html)  MyBatis 是一个可以自定义 SQL、存储过程和高级映射的持久层框架。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1085.讲下 MyBatis 的缓存

> 原文：[https://zwmst.com/5462.html](https://zwmst.com/5462.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:21:48+08:00"> 2021-10-25 </time> ](https://zwmst.com/5462.html)  MyBatis 的缓存分为一级缓存和二级缓存,一级缓存放在 session 里面,默认就有,二级缓存放在它的命名空间里,默认是不打开的,使用二级缓存属性类需要实现 Serializable 序列化接口(可用来保存对象的状态),可在它的映射文件中配置<cache/*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1086.Mybatis 是如何进行分页的？分页插件的原理是什么？

> 原文：[https://zwmst.com/5464.html](https://zwmst.com/5464.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:24:18+08:00"> 2021-10-25 </time> ](https://zwmst.com/5464.html)  1.  Mybatis 使用 RowBounds 对象进行分页，也可以直接编写 sql 实现分页，也可以使用Mybatis 的分页插件。
2.  分页插件的原理：实现 Mybatis 提供的接口，实现自定义插件，在插件的拦截方法内拦截待执行的 sql，然后重写 sql。
    举例：

    ```
    select * from student，拦截 sql 后重写为：select t.* from （select * from student）t limit 0，10
    ```*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1087.简述 Mybatis 的插件运行原理，以及如何编写一个插件？

> 原文：[https://zwmst.com/5466.html](https://zwmst.com/5466.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:26:23+08:00"> 2021-10-25 </time> ](https://zwmst.com/5466.html)  1.  Mybatis 仅可以编写针对 ParameterHandler、ResultSetHandler、StatementHandler、Executor 这 4 种接口的插件，Mybatis 通过动态代理，为需要拦截的接口生成代理对象以实现接口方法拦截功能，每当执行这 4 种接口对象的方法时，就会进入拦截方法，具体就是InvocationHandler 的 invoke()方法，当然，只会拦截那些你指定需要拦截的方法。
2.  实现 Mybatis 的 Interceptor 接口并复写 intercept()方法，然后在给插件编写注解，指定要拦截哪一个接口的哪些方法即可，记住，别忘了在配置文件中配置你编写的插件。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1088.Mybatis 动态 sql 是做什么的？都有哪些动态 sql？能简述一下动态 sql 的执行原理不？

> 原文：[https://zwmst.com/5468.html](https://zwmst.com/5468.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:27:26+08:00"> 2021-10-25 </time> ](https://zwmst.com/5468.html)  1.  Mybatis 动态 sql 可以让我们在 Xml 映射文件内，以标签的形式编写动态 sql，完成逻辑判断和动态拼接 sql 的功能。
2.  Mybatis 提供了 9 种动态 sql 标签：
    trim|where|set|foreach|if|choose|when|otherwise|bind。
3.  其执行原理为，使用 OGNL 从 sql 参数对象中计算表达式的值，根据表达式的值动态拼接 sql，以此来完成动态 sql 的功能。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1089.#{}和${}的区别是什么？

> 原文：[https://zwmst.com/5470.html](https://zwmst.com/5470.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:28:52+08:00"> 2021-10-25 </time> ](https://zwmst.com/5470.html)  1.  # {}是预编译处理，${}是字符串替换。

2.  Mybatis 在处理#{}时，会将 sql 中的#{}替换为?号，调用 PreparedStatement 的 set 方法来赋值；
3.  Mybatis 在处理${}时，就是把${}替换成变量的值。
4.  使用#{}可以有效的防止 SQL 注入，提高系统安全性。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1090.为什么说 Mybatis 是半自动 ORM 映射工具？它与全自动的区别在哪里？

> 原文：[https://zwmst.com/5472.html](https://zwmst.com/5472.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:35:56+08:00"> 2021-10-25 </time> ](https://zwmst.com/5472.html)  Hibernate 属于全自动 ORM 映射工具，使用 Hibernate 查询关联对象或者关联集合对象时，可以根据对象关系模型直接获取，所以它是全自动的。而 Mybatis 在查询关联对象或关联集合对象时，需要手动编写 sql 来完成，所以，称之为半自动 ORM 映射工具。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1091.、Mybatis 是否支持延迟加载？如果支持，它的实现原理是什么？

> 原文：[https://zwmst.com/5474.html](https://zwmst.com/5474.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:39:01+08:00"> 2021-10-25 </time> ](https://zwmst.com/5474.html)  1.  Mybatis 仅支持 association 关联对象和 collection 关联集合对象的延迟加载，association指的就是一对一，collection 指的就是一对多查询。在 Mybatis 配置文件中，可以配置是否启用延迟加载 lazyLoadingEnabled=true|false。
2.  它的原理是，使用 CGLIB 创建目标对象的代理对象，当调用目标方法时，进入拦截器方法，比如调用 a.getB().getName()，拦截器 invoke()方法发现 a.getB()是 null 值，那么就会单独发送事先保存好的查询关联 B 对象的 sql，把 B 查询上来，然后调用 a.setB(b)，于是 a 的对象 b 属性就有值了，接着完成 a.getB().getName()方法的调用。这就是延迟加载的基本原理。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1092.MyBatis 与 Hibernate 有哪些不同？

> 原文：[https://zwmst.com/5476.html](https://zwmst.com/5476.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:40:13+08:00"> 2021-10-25 </time> ](https://zwmst.com/5476.html)  1.  Mybatis 和 hibernate 不同，它不完全是一个 ORM 框架，因为 MyBatis 需要程序员自己编写 Sql 语句，不过 mybatis 可以通过 XML 或注解方式灵活配置要运行的 sql 语句，并将java 对象和 sql 语句映射生成最终执行的 sql，最后将 sql 执行的结果再映射生成 java 对象。
2.  Mybatis 学习门槛低，简单易学，程序员直接编写原生态 sql，可严格控制 sql 执行性能，灵活度高，非常适合对关系数据模型要求不高的软件开发，例如互联网软件、企业运营类软件等，因为这类软件需求变化频繁，一但需求变化要求成果输出迅速。但是灵活的前提是 mybatis 无法做到数据库无关性，如果需要实现支持多种数据库的软件则需要自定义多套 sql 映射文件，工作量大。
3.  Hibernate 对象/关系映射能力强，数据库无关性好，对于关系模型要求高的软件（例如需求固定的定制化软件）如果用 hibernate 开发可以节省很多代码，提高效率。但是Hibernate 的缺点是学习门槛高，要精通门槛更高，而且怎么设计 O/R 映射，在性能和对象模型之间如何权衡，以及怎样用好 Hibernate 需要具有很强的经验和能力才行。总之，按照用户的需求在有限的资源环境下只要能做出维护性、扩展性良好的软件架构都是好架构，所以框架只有适合才是最好。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1093.MyBatis 的好处是什么？

> 原文：[https://zwmst.com/5478.html](https://zwmst.com/5478.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:41:13+08:00"> 2021-10-25 </time> ](https://zwmst.com/5478.html)  1.  MyBatis 把 sql 语句从 Java 源程序中独立出来，放在单独的 XML 文件中编写，给程序的维护带来了很大便利。
2.  MyBatis 封装了底层 JDBC API 的调用细节，并能自动将结果集转换成 Java Bean 对象，大大简化了 Java 数据库编程的重复工作。
3.  因为 MyBatis 需要程序员自己去编写 sql 语句，程序员可以结合数据库自身的特点灵活控制 sql 语句，因此能够实现比 Hibernate 等全自动 orm 框架更高的查询效率，能够完成复杂查询。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1094.简述 Mybatis 的 Xml 映射文件和 Mybatis 内部数据结构之间的映射关系？

> 原文：[https://zwmst.com/5480.html](https://zwmst.com/5480.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:42:16+08:00"> 2021-10-25 </time> ](https://zwmst.com/5480.html)  Mybatis 将所有 Xml 配置信息都封装到 All-In-One 重量级对象 Configuration 内部。在Xml 映射文件中，`<parameterMap>`标签会被解析为 ParameterMap 对象，其每个子元素会被解析为 ParameterMapping 对象。`<resultMap>`标签会被解析为 ResultMap 对象，其每个子元素会被解析为 ResultMapping 对象。每一个`<select>、<insert>、<update>、<delete>`标签均会被解析为 MappedStatement 对象，标签内的 sql 会被解析为 BoundSql 对象。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1095.什么是 MyBatis 的接口绑定,有什么好处？

> 原文：[https://zwmst.com/5482.html](https://zwmst.com/5482.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:44:22+08:00"> 2021-10-25 </time> ](https://zwmst.com/5482.html)  接口映射就是在 MyBatis 中任意定义接口,然后把接口里面的方法和 SQL 语句绑定,我们直接调用接口方法就可以,这样比起原来了 SqlSession 提供的方法我们可以有更加灵活的选择和设置.*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1096.接口绑定有几种实现方式,分别是怎么实现的?

> 原文：[https://zwmst.com/5484.html](https://zwmst.com/5484.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:45:36+08:00"> 2021-10-25 </time> ](https://zwmst.com/5484.html)  接口绑定有两种实现方式,一种是通过注解绑定,就是在接口的方法上面加上@Select@Update 等注解里面包含 Sql 语句来绑定,另外一种就是通过 xml 里面写 SQL 来绑定,在这种情况下,要指定 xml 映射文件里面的 namespace 必须为接口的全路径名.*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1097.什么情况下用注解绑定,什么情况下用 xml 绑定？

> 原文：[https://zwmst.com/5486.html](https://zwmst.com/5486.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:46:38+08:00"> 2021-10-25 </time> ](https://zwmst.com/5486.html)  当 Sql 语句比较简单时候,用注解绑定；当 SQL 语句比较复杂时候,用 xml 绑定,一般用xml 绑定的比较多*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1098.MyBatis 实现一对一有几种方式?具体怎么操作的？

> 原文：[https://zwmst.com/5488.html](https://zwmst.com/5488.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:47:33+08:00"> 2021-10-25 </time> ](https://zwmst.com/5488.html)  有联合查询和嵌套查询,联合查询是几个表联合查询,只查询一次,通过在 resultMap 里面配置 association 节点配置一对一的类就可以完成;嵌套查询是先查一个表,根据这个表里面的结果的外键 id,去再另外一个表里面查询数据,也是通过 association 配置,但另外一个表的查询通过 select 属性配置。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1099.Mybatis 能执行一对一、一对多的关联查询吗？都有哪些实现方式，以及它们之间的区 别？

> 原文：[https://zwmst.com/5490.html](https://zwmst.com/5490.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:48:46+08:00"> 2021-10-25 </time> ](https://zwmst.com/5490.html)  能，Mybatis 不仅可以执行一对一、一对多的关联查询，还可以执行多对一，多对多的关联查询，多对一查询，其实就是一对一查询，只需要把 selectOne()修改为 selectList()即可；多对多查询，其实就是一对多查询，只需要把 selectOne()修改为 selectList()即可。
关联对象查询，有两种实现方式，一种是单独发送一个 sql 去查询关联对象，赋给主对象，然后返回主对象。另一种是使用嵌套查询，嵌套查询的含义为使用 join 查询，一部分列是 A 对象的属性值，另外一部分列是关联对象 B 的属性值，好处是只发一个 sql 查询，就可以把主对象和其关联对象查出来。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1100.MyBatis 里面的动态 Sql 是怎么设定的?用什么语法?

> 原文：[https://zwmst.com/5492.html](https://zwmst.com/5492.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:49:34+08:00"> 2021-10-25 </time> ](https://zwmst.com/5492.html)  MyBatis 里面的动态 Sql 一般是通过 if 节点来实现,通过 OGNL 语法来实现,但是如果要写的完整,必须配合 where,trim 节点,where 节点是判断包含节点有内容就插入 where,否则不插入,trim 节点是用来判断如果动态语句是以 and 或 or 开始,那么会自动把这个 and 或者 or取掉。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1101.Mybatis 是如何将 sql 执行结果封装为目标对象并返回的？都有哪些映射形式？

> 原文：[https://zwmst.com/5494.html](https://zwmst.com/5494.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-25T23:50:35+08:00"> 2021-10-25 </time> ](https://zwmst.com/5494.html)  第一种是使用`<resultMap>`标签，逐一定义列名和对象属性名之间的映射关系。
第二种是使用 sql 列的别名功能，将列别名书写为对象属性名，比如 T_NAME AS NAME，对象属性名一般是 name，小写，但是列名不区分大小写，Mybatis 会忽略列名大小写，智能找到与之对应对象属性名，你甚至可以写成 T_NAME AS NaMe Mybatis 一样可以正常工作。
有了列名与属性名的映射关系后，Mybatis 通过反射创建对象，同时使用反射给对象的属性逐一赋值并返回，那些找不到映射关系的属性，是无法完成赋值的。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1102.Xml 映射文件中，除了常见的 select|insert|updae|delete 标签之外，还有哪些标签？

> 原文：[https://zwmst.com/5497.html](https://zwmst.com/5497.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:00:03+08:00"> 2021-10-25 </time> ](https://zwmst.com/5497.html)  还有很多其他的标签，`<resultMap>、<parameterMap>、<sql>、<include>、<selectKey>`，加上动态 sql 的 9 个标签，trim|where|set|foreach|if|choose|when|otherwise|bind 等，其中`<sql>`为 sql 片段标签，通过`<include>`标签引入 sql 片段，`<selectKey>`为不支持自增的主键生成策略标签。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1103.当实体类中的属性名和表中的字段名不一样，如果将查询的结果封装到指定 pojo？

> 原文：[https://zwmst.com/5499.html](https://zwmst.com/5499.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:01:06+08:00"> 2021-10-25 </time> ](https://zwmst.com/5499.html)  1.  通过在查询的 sql 语句中定义字段名的别名。
2.  通过`<resultMap>`来映射字段名和实体类属性名的一一对应的关系。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1104.模糊查询 like 语句该怎么写

> 原文：[https://zwmst.com/5502.html](https://zwmst.com/5502.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:01:52+08:00"> 2021-10-25 </time> ](https://zwmst.com/5502.html)  1.  在 java 中拼接通配符，通过#{}赋值
2.  在 Sql 语句中拼接通配符 （不安全 会引起 Sql 注入）*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1105.通常一个 Xml 映射文件，都会写一个 Dao 接口与之对应, Dao 的工作原理，是否可以重 载？

> 原文：[https://zwmst.com/5504.html](https://zwmst.com/5504.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:02:36+08:00"> 2021-10-25 </time> ](https://zwmst.com/5504.html)  不能重载，因为通过 Dao 寻找 Xml 对应的 sql 的时候全限名+方法名的保存和寻找策略。接口工作原理为 jdk 动态代理原理，运行时会为 dao 生成 proxy，代理对象会拦截接口方法，去执行对应的 sql 返回数据。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1106.Mybatis 映射文件中，如果 A 标签通过 include 引用了 B 标签的内容，请问，B 标签能 否定义在 A 标签的后面，还是说必须定义在 A 标签的前面？

> 原文：[https://zwmst.com/5506.html](https://zwmst.com/5506.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:03:50+08:00"> 2021-10-25 </time> ](https://zwmst.com/5506.html)  虽然 Mybatis 解析 Xml 映射文件是按照顺序解析的，但是，被引用的 B 标签依然可以定义在任何地方，Mybatis 都可以正确识别。原理是，Mybatis 解析 A 标签，发现 A 标签引用了 B 标签，但是 B 标签尚未解析到，尚不存在，此时，Mybatis 会将 A 标签标记为未解析状态，然后继续解析余下的标签，包含 B 标签，待所有标签解析完毕，Mybatis 会重新解析那些被标记为未解析的标签，此时再解析 A 标签时，B 标签已经存在，A 标签也就可以正常解析完成了。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1107.Mybatis 的 Xml 映射文件中，不同的 Xml 映射文件，id 是否可以重复？

> 原文：[https://zwmst.com/5508.html](https://zwmst.com/5508.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:04:33+08:00"> 2021-10-25 </time> ](https://zwmst.com/5508.html)  不同的 Xml 映射文件，如果配置了 namespace，那么 id 可以重复；如果没有配置namespace，那么 id 不能重复；毕竟 namespace 不是必须的，只是最佳实践而已。原因就是 namespace+id 是作为 Map<String, MappedStatement>的 key 使用的，如果没有namespace，就剩下 id，那么，id 重复会导致数据互相覆盖。有了 namespace，自然 id 就可以重复，namespace 不同，namespace+id 自然也就不同。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1108.Mybatis 中如何执行批处理？

> 原文：[https://zwmst.com/5510.html](https://zwmst.com/5510.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:05:11+08:00"> 2021-10-25 </time> ](https://zwmst.com/5510.html)  使用 BatchExecutor 完成批处理。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1109.Mybatis 都有哪些 Executor 执行器？它们之间的区别是什么？

> 原文：[https://zwmst.com/5512.html](https://zwmst.com/5512.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:09:08+08:00"> 2021-10-25 </time> ](https://zwmst.com/5512.html)  Mybatis 有三种基本的 Executor 执行器，SimpleExecutor、ReuseExecutor、BatchExecutor。1）SimpleExecutor：每执行一次 update 或 select，就开启一个 Statement 对象，用完立刻关闭 Statement 对象。2）ReuseExecutor：执行 update 或 select，以 sql 作为key 查找 Statement 对象，存在就使用，不存在就创建，用完后，不关闭 Statement 对象，而是放置于 Map3）BatchExecutor：完成批处理。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1110.Mybatis 中如何指定使用哪一种 Executor 执行器？

> 原文：[https://zwmst.com/5514.html](https://zwmst.com/5514.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:09:47+08:00"> 2021-10-25 </time> ](https://zwmst.com/5514.html)  在 Mybatis 配置文件中，可以指定默认的 ExecutorType 执行器类型，也可以手动给DefaultSqlSessionFactory 的创建 SqlSession 的方法传递 ExecutorType 类型参数。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1111.Mybatis 执行批量插入，能返回数据库主键列表吗？

> 原文：[https://zwmst.com/5516.html](https://zwmst.com/5516.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:10:28+08:00"> 2021-10-25 </time> ](https://zwmst.com/5516.html)  能，JDBC 都能，Mybatis 当然也能。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1112.Mybatis 是否可以映射 Enum 枚举类？

> 原文：[https://zwmst.com/5519.html](https://zwmst.com/5519.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:11:29+08:00"> 2021-10-25 </time> ](https://zwmst.com/5519.html)  Mybatis 可以映射枚举类，不单可以映射枚举类，Mybatis 可以映射任何对象到表的一列上。映射方式为自定义一个 TypeHandler，实现 TypeHandler 的 setParameter()和getResult()接口方法。TypeHandler 有两个作用，一是完成从 javaType 至 jdbcType 的转换，二是完成 jdbcType 至 javaType 的转换，体现为 setParameter()和 getResult()两个方法，分别代表设置 sql 问号占位符参数和获取列查询结果。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1113.如何获取自动生成的(主)键值？

> 原文：[https://zwmst.com/5521.html](https://zwmst.com/5521.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:12:21+08:00"> 2021-10-25 </time> ](https://zwmst.com/5521.html)  配置文件设置 usegeneratedkeys 为 true*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1114.在 mapper 中如何传递多个参数？

> 原文：[https://zwmst.com/5523.html](https://zwmst.com/5523.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:13:14+08:00"> 2021-10-25 </time> ](https://zwmst.com/5523.html)  1.  直接在方法中传递参数，xml 文件用#{0} #{1}来获取
2.  使用 @param 注解:这样可以直接在 xml 文件中通过#{name}来获取*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1115.resultType resultMap 的区别？

> 原文：[https://zwmst.com/5525.html](https://zwmst.com/5525.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:13:58+08:00"> 2021-10-25 </time> ](https://zwmst.com/5525.html)  1.  类的名字和数据库相同时，可以直接设置 resultType 参数为 Pojo 类
2.  若不同，需要设置 resultMap 将结果名字和 Pojo 名字进行转换*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1116.使用 MyBatis 的 mapper 接口调用时有哪些要求？

> 原文：[https://zwmst.com/5527.html](https://zwmst.com/5527.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:15:12+08:00"> 2021-10-25 </time> ](https://zwmst.com/5527.html)  1.  Mapper 接口方法名和 mapper.xml 中定义的每个 sql 的 id 相同
2.  Mapper 接口方法的输入参数类型和 mapper.xml 中定义的每个 sql 的 parameterType 的类型相同
3.  Mapper 接口方法的输出参数类型和 mapper.xml 中定义的每个 sql 的 resultType 的类型相同
4.  Mapper.xml 文件中的 namespace 即是 mapper 接口的类路径。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1117.Mybatis 比 IBatis 比较大的几个改进是什么？

> 原文：[https://zwmst.com/5531.html](https://zwmst.com/5531.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:16:35+08:00"> 2021-10-25 </time> ](https://zwmst.com/5531.html)  1.  有接口绑定,包括注解绑定 sql 和 xml 绑定 Sql
2.  动态 sql 由原来的节点配置变成 OGNL 表达式 3） 在一对一,一对多的时候引进了association,在一对多的时候引入了 collection 节点,不过都是在 resultMap 里面配置*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1118.IBatis 和 MyBatis 在核心处理类分别叫什么？

> 原文：[https://zwmst.com/5533.html](https://zwmst.com/5533.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:17:14+08:00"> 2021-10-25 </time> ](https://zwmst.com/5533.html)  IBatis 里面的核心处理类交 SqlMapClient,MyBatis 里面的核心处理类叫做 SqlSession。*
<!--yml
category: 未分类
date: 0001-01-01 00:00:00
-->

# 1119.IBatis 和 MyBatis 在细节上的不同有哪些？

> 原文：[https://zwmst.com/5535.html](https://zwmst.com/5535.html)

   [ *MyBatis* ](https://zwmst.com/mybatis)*[ <time datetime="2021-10-26T00:18:38+08:00"> 2021-10-25 </time> ](https://zwmst.com/5535.html)  1.  在 sql 里面变量命名有原来的#变量# 变成了#{变量}
2.  原来的$变量$变成了${变量}
3.  原来在 sql 节点里面的 class 都换名字交 type
4.  原来的 queryForObject queryForList 变成了 selectOne selectList5）原来的别名设置在映射文件里面放在了核心配置文件里*