# Neo4j

## 1. Neo4j是什么

**Neo4j** 是一个高性能的 ``NoSQL``图形数据库，它将结构化数据存储在网络（从数学角度叫做图）上而不是表中。Neo4j 也可以被看作是一个高性能的图引擎，该引擎具有成熟数据库的所有特性。

<img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20230621104749.png" alt="image-20230612092138180" style="zoom:50%;" />  

> 你和任何一个陌生人之间所间隔的人不会超过六个
> 即最多通过6个中间人你就能够认识任何一个陌生人

> **NoSQL**(**Not only SQL**)是对不同于传统的关系数据库的数据库管理系统的统称，即广义地来说可以把所有不是关系型数据库的数据库统称为**NoSQL**。

## 2. Neo4j适用场景

- **最短路径**：使用Neo4j计算两点之间的最短路径。

  > [空间数据_neo4j 空间数据_](https://blog.csdn.net/sikh_0529/article/details/127247778)
  >
  > [ neo4j结合gds实现最短路径算法](https://blog.csdn.net/weixin_43632687/article/details/130523276?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2~default~YuanLiJiHua~Position-2-130523276-blog-83110854.235^v38^pc_relevant_sort_base3&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2~default~YuanLiJiHua~Position-2-130523276-blog-83110854.235^v38^pc_relevant_sort_base3&utm_relevant_index=3)

  > >- **社交媒体和社交网络图**： 以Neo4j图形数据库为基础，社交网络APP可以轻松处理社交关系或根据活动推断关系。
  > >- **知识图谱**： 基于Neo4j数据类型以及图形的强大搜索功能， 由知识点之间的关系建立知识图，帮助用户搜索到关联的知识 。
  > >- **反欺诈多维关联分析**： 通过图分析可以清楚的知道洗钱网络及相关嫌疑，例如对用户所使用的账号、发生交易时的IP地址、MAC地址、手机IMEI号等进行关联分析
  > >- **企业关系图谱**： 企业在日常经营中，与客户、合作伙伴、渠道方、投资者都会打交道，这也决定了企业对社会各个领域都广有涉猎，呈现面错综复杂，因此可以通过Neo4j的企业数据图谱来查询，层层挖掘信息。
  > >- **推荐**：基于Neo4j的优势进行个性化推荐， 通过分析用户有哪些朋友、用户朋友喜好的产品、用户的浏览记录等关系信息推测用户的喜好进而为用户推荐商品

## 3. Neo4j如何使用

### Neo4j是怎样存储错综复杂的用户关系的?

<img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047491.png" alt="image-20230612093942116" style="zoom:50%;" /> 

* 节点：节点通常用来表示实体，是组成图的最小单位。一个节点就类似一个实体类的具体对象。节点存在各种属性，例如姓名，id，标签等，但是必须确定某一属性为唯一性，类似**mysql**主键，该节点的该属性值具有唯一性且非空。
* 标签：标签用于分类节点，节点可以没有标签但是也可以存在多个标签。类似于学生类、员工类等等，如果一个节点又是学生又是员工，那这个节点就存在多个标签。
* 关系：关系连接两个节点。关系具有方向性。被关系连接的两个节点，其中关系的起始节点被称为**出节点**，关系的终止节点被称为**入节点**。同时，一个节点的**出度**是指这个节点被多少关系作为出节点，同理，**入度**是指被多少个关系作为入节点。特别的是，一个节点可以有指向自己的关系。

* 关系类型：类似节点标签，但是关系有且仅有一种关系类型。上图节点1到节点2如果是朋友，同学多种关系，那就是存在多个关系线，不能在一个关系线上存在多个关系。
* 路径与遍历：在图中，查询过程是路径搜索与遍历的过程。类似六个陌生人，查询你的朋友，搜索长度为1，查询你朋友的朋友，搜索长度为2。

### Neo4j安装

Neo4j的安装主要是有两个，一个是**desktop**版本，也就是桌面版，更容易操作，界面更加清晰，但是因为加密端弄了半天没弄好就下了**server**版本。

**server**版本主要是提供了一个 服务器的功能，运行服务可以在本地**7474**端口查看相应内容。

#### 1. 安装JDK以及Neo4j

**Neo4j**是一个基于**Java**的图形数据库和分析平台，它需要一个兼容的**Java**虚拟机（**JVM**）来运行。因此，在安装**Neo4j**之前，必须安装**JDK** 。并且Neo4j和jdk必须匹配，我们常用的**jdk**是**java8**，那么**Neo4j**对应的版本是**3.X**，找一个**3.X**中最新的版本就行了。我下载的是**3.5.8**版本。

> Neo4j历史版本下载连接：https://we-yun.com/doc/neo4j/

下载之后到你需要的文件夹下解压即可。然后配置环境变量，**bin**文件夹。

以管理员身份运行**cmd**，命令行处输入**neo4j.bat console**。Neo4j启动成功之后打开**http://localhost:7474/**则会出现Neo4j的相关界面。默认的用户名和密码均为**neo4j**，我将密码修改为了**123**.

#### 2. Neo4j使用

Neo4j有两种方式做图，一种是直接创建节点、关系等，另一种是导入**csv**文件直接生成图。我使用的是导入。

首先制作三张**csv**表文件。

第一个实体：  
<img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047492.png" alt="image-20230612105114509" style="zoom:50%;" /> 

第二个实体：  
<img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047493.png" alt="image-20230612105131269" style="zoom:50%;" />

关系文件：  
<img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047494.png" alt="image-20230612105155735" style="zoom:50%;" />

> 注意：因为**csv**文件含有中文，所以需要修改编码为**UTF-8**。

将三个文件放入**import**文件夹。然后打开**conf**配置文件，将第九行改为你将创建的数据库名称。

然后在**cmd**中输入导入命令

```
neo4j-admin import --mode=csv --database=onepice.db --nodes D:\neo4j\neo4j-community-3.5.5\import\friends.csv --nodes D:\neo4j\neo4j-community-3.5.5\import\node.csv --relationships D:\neo4j\neo4j-community-3.5.5\import\rel.csv

```

然后运行**Neo4j**

```
neo4j.bat console
```

浏览器输入**http://localhost:7474/**查看如下：

<img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047495.png" alt="image-20230612115338839" style="zoom:50%;" /> 





### Neo4j实例：两个地点之间的最近距离

1. 创建一个新的数据库 **distance.db**

   >conf文件中修改数据库名称即可。

2. 下载**gds**的相关版本**jar**包，并将jar包复制到**plugins**文件夹下。

   > 对于**Neo4j 3.X**版本，下载**gds1.1.1**版本 **jar**包

3. 运行**Neo4j**服务，测试**gds**安装是否成功

   ```
   RETURN gds.version()
   ```

4. 新建几个节点作为地点

   ```
   create (A:Line{name:"A"}) 
   create (B:Line{name:"B"}) 
   create (C:Line{name:"C"}) 
   create (D:Line{name:"D"}) 
   create (E:Line{name:"E"}) 
   create (A)-[:LINKED_TO{weight:10}]->(B) 
   create (A)-[:LINKED_TO{weight:33}]->(C) 
   create (A)-[:LINKED_TO{weight:35}]->(D) 
   create (B)-[:LINKED_TO{weight:20}]->(C) 
   create (C)-[:LINKED_TO{weight:28}]->(D) 
   create (C)-[:LINKED_TO{weight:6}]->(E) 
   create (D)-[:LINKED_TO{weight:40}]->(E) 
   ```

   <img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047496.png" alt="image-20230612173120384" style="zoom: 50%;" /> 

5. 查询A->E的最近距离

   ```
   call gds.graph.create("ellisweight","Line","LINKED_TO",{relationshipProperties:[{weight:"weight"}]})
   
   MATCH(a:Line{name:"A"})
   MATCH(e:Line{name:"E"})
   call gds.alpha.shortestPath.stream("ellisweight",{startNode:a,endNode:e,relationshipWeightProperty:"weight"})
   yield nodeId,cost
   return gds.util.asNode(nodeId).name,cost
   ```

   <img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047497.png" alt="image-20230612173253077" style="zoom: 50%;" />    

   
   
   <img src="https://wangfangdong.oss-cn-hangzhou.aliyuncs.com/neo4j/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_202306211047498.png" alt="image-20230612173305325" style="zoom:50%;" />  





