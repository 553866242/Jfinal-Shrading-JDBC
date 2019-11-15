### Jfinal整合Shrading-JDBC,实现分表功能和数据库脱敏

首先我们要先明确这样一个业务场景，如果生产上某个表的数据在100w+，那么sql语句进行表操作，还不会出现什么瓶颈问题，如果数据量再增加到500w+，可以通过索引，备份等方式，减少数据库的单表压力。如果继续增加到1000w。或者单表一天的数据量就能达到1000w。那么建议索引就无法在解决在这个问题。这时候，我们就需要`通过分表的操作，来降低单表的压力。`

#### 实现思路：
  1. 上面我们已经知道了问题所在，下面来分析一下解决方案。既然单个表无法满足生产上是数据量，那么就需要创建多个表。而如何将多个表进行关联起来，我们就需要用到分表组件：ShardingSphere中的`sharding-jdbc`模块。


#### 解决方案：（全部代码会在文末全部提供）
  1.首先，我们数据库中只有一张表 `t_blog`。假设这张表的数据量已经达到的1000w的级别。接下来我们在创建8张表，表名为`t_blog_x`，这8张表的结构和原来的完全一样，这8张表我们把它称为`真实表`，而原来的`t_blog`表，我们称为`逻辑表`。

分表后，数据库结构如下：
![Alt text](/src/main/webapp/images/数据库.PNG)

### 使用方法：
1. 先执行blog.sql脚本
2. 执行DemoConfig.java文件，来启动项目 
3. 执行 http://127.0.0.1:80/blog/save/ 来进行测试即可

![Alt text](/src/main/webapp/images/example.PNG)

4.数据库中数据如下

![Alt text](/src/main/webapp/images/first.PNG)