# 《监管平台》项目所得



## 学会了什么 ✔

1. **springboot**项目中如何增加依赖

   ![image-20230524155803753](C:\Users\14573\AppData\Roaming\Typora\typora-user-images\image-20230524155803753.png)

   > 个别依赖可以不需要添加版本,由**springboot**决定.

2. **springboot**项目如何融合**springmvc**,**mybatis-plus**,**druid**,等

    * **springmvc**是在新建springboot项目时添加**springweb**即可,**mybatis-plus**和**druid**则需要单独添加依赖

3. 完整的项目结构

   ![image-20230524160505518](C:\Users\14573\AppData\Roaming\Typora\typora-user-images\image-20230524160505518.png)

    * **config** 包中存放配置类,需加注解**@Configuration**

    * **constants **包中存放枚举类

    * **controller** 包中存放控制器,springboot项目中使用注解**@RestController**

    * ❓**dto**包中存放的是单个或多个项目库表中得到的字段组成的类

    * **entity** 包中存放的是根据库表生成的实体类

    * **mapper** 包中存放的是**mapper**接口继承于**BaseMapper<>**使用注解**@mapper**,包含**xml**子包存放相应的**xml**文件

      > **mapper**接口和**xml**文件要配置好

    * **service** 包中存放的是项目服务层代码继承于**Iservice<>**,含有子包**impl**,存放相应的实现类需要使用注解**@service**

      > ![image-20230524164513479](C:\Users\14573\AppData\Roaming\Typora\typora-user-images\image-20230524164513479.png) 一般命名时前面加"**I**"
      >
      > ![image-20230524165051415](C:\Users\14573\AppData\Roaming\Typora\typora-user-images\image-20230524165051415.png) 实现类中需要继承于**ServiceImpl<mapper接口,实体类>**

    * ❓**vo** 包中存放视图对象用于前端展示

4. 纯后端的代码实现与**ApiFox**的测试

    * 根据原型界面编写接口,无直接前端页面展示,所以很多接口功能需要想象着去做,需要一定经验.

    * 在**controller**层编写接口功能以及设置注解**@RequestMapping**,在ApiFox进行测试

      > **ApiFox**需要注意以下几点 :
      >
      > 1. 首先应在在数据模型中增加实体数据模型
      >
      > 2. **Get**请求需要设置好返回响应
      >
      > 3. **Post**请求需要在请求参数中设置**json**参数
      >
      > 4. 一个接口测试成功需要修改接口状态为已发布

    * 基础的**CRUD**通过**mybatis-plus**实现(由自动生成代码插件生成代码),只需要在原基础上修改一下即可

    * **mybatis-plus**无法直接实现的查询需要自己编写查询语句,一般是通过**service**接口编写抽象方法,在实现类中完成相应功能,查询语句则写在**mapper.xml**文件中.

    * **jeecgboot**封装了一个返回接口返回对象**Result<T>**,对于全部的**controller**层方法返回的对象都需要被这个返回接口对象封装一下.

    * **lombok**,使用**@Data**等注解可以简化代码

5. 项目分工与**Git**

    * 项目开始时需创建自己的分支,将编写的以及后续修改的代码推送到自己的分支,在推送代码前后都需要更新项目代码.

6. 项目代码流程

    1. 根据产品原型确定每个页面的功能.
    2. 针对功能模块进行数据库设计并建表.
    3. 使用合适的**java**框架搭建项目框架.
    4. 根据数据库表以及代码生成工具完成**entity**,**controllert**,**mapper**以及**service**的基础开发.
    5. 根据功能对生成的代码进行修改优化.
    6. 无法生成的功能需要自己编写**sql**以及在**service**层编写方法进行实现.
    7. 代码完成自己需要在**ApiFox**进行测试.
    8. 测试通过再次查阅代码,消除没使用的jar包等.
    9. 与前端联调完成整体项目.





## 疑问 (已解答)❗

1. 为什么新增和更新都使用**post**请求

   > 历史遗留问题,更新一般使用put请求,新增使用post请求

2. **dto**层和**vo**层有什么不一样

   > dto层一般是service进行维护,vo则是前端展示的数据



## 下一步学习问题   ❓

1. **maven**导入是**jar**包? 如果需要导入自己的项目作为依赖,应该如何使用**maven**进行导入？

   > 1. Maven 导入的依赖通常都是 jar 包。
   > 2. 想将自己的项目作为依赖导入到另一个项目中，需要先将自己的项目打包并安装到本地 Maven 仓库或部署到远程 Maven 仓库。然后，在需要使用该依赖的项目的 `pom.xml` 文件中添加相应的依赖信息，包括 `groupId`、`artifactId` 和 `version`。

1. **maven**常用命令,如**mvn clean**,**mvn test**的学习？

   > - `mvn clean`：此命令用于清理项目目录中的 `target` 文件夹，删除所有之前构建生成的文件。
   > - `mvn compile`：此命令用于编译项目的源代码。
   > - `mvn test`：此命令用于运行项目的单元测试。
   > - `mvn package`：此命令用于将项目打包为 jar 或 war 文件。
   > - `mvn install`：此命令用于将项目打包并安装到本地 Maven 仓库，以便其他项目可以将其作为依赖使用。
   > - `mvn deploy`：此命令用于将项目打包并部署到远程 Maven 仓库。

2. **spring**常用注解理解？**@RestController**和**@Controller**的区别,**@Resource**和**@Autowired**区别 ？**@Configuration**注解如何使用以及理解？

   > **@RestController**和**@Controller**的区别
   >
   > 1. `@Controller` 和 `@RestController` 都是用于标记控制器类的注解
   > 2. `@RestController` 是一个特殊的控制器注解，它是 `@Controller` 和 `@ResponseBody` 注解的组合。使用该注解之后所有方法的返回值都会被转换为 JSON 或 XML 并写入响应体中。
   > 3. `@Controller` 用于定义通用的控制器，支持返回视图和数据；而 `@RestController` 用于定义 RESTful 风格的控制器，只支持返回数据。
   >
   > **@Resource**和**@Autowired**区别
   >
   > 1. `@Autowired` 默认按类型进行自动装配，可以通过 `@Qualifier` 注解来指定 bean 的名称；而 `@Resource` 默认按名称进行自动装配，可以通过 `name` 属性来指定 bean 的名称。基本上可以全部使用`@Resource`。

3. 枚举类的使用场景，**枚举类**与**普通类**的不同？

   > `枚举类`与`普通类`的不同
   >
   > 1. 枚举类是一种特殊的类，它用于定义一组固定的常量。与普通类不同，枚举类中的每个实例都是预先定义好的，并且实例数量是固定的。
   >
   > 枚举类的使用场景
   >
   > 1. 枚举类通常用于表示一组固定的值，例如星期、月份、颜色等。

4. 公司目前使用的**PostgreSQL**数据库和**MYSQL**数据库有何不同？

5. **lombok**插件的使用,各个注解都是代表什么？

   > **lombok**插件的使用
   >
   > * 要使用 Lombok，需要在开发环境中安装 Lombok 插件，并在项目中添加 Lombok 依赖.
       >
       >   ```
   >   <dependency>
   >       <groupId>org.projectlombok</groupId>
   >       <artifactId>lombok</artifactId>
   >       <version>1.18.22</version>
   >   </dependency>
   >   ```
   >
   > **lombok**各个注解都是代表什么
   >
   > - `@Data`：用在类上，自动生成 getter、setter、toString、equals 和 hashCode 等方法。
   > - `@Getter` / `@Setter`：用在属性上，自动生成 getter 和 setter 方法。
   > - `@ToString`：用在类上，自动生成 toString 方法。
   > - `@EqualsAndHashCode`：用在类上，自动生成 equals 和 hashCode 方法。
   > - `@NoArgsConstructor` / `@RequiredArgsConstructor` / `@AllArgsConstructor`：用在类上，自动生成无参构造函数、必需参数构造函数和全参构造函数。
   > - `@Builder`：用在类、构造器或方法上，为您提供复杂的 builder API。
   > - `@SneakyThrows`：用在方法上，自动抛出受检异常，而无需显式在方法上使用 throws 语句。
   > - `@Synchronized`：用在方法上，将方法声明为同步的，并自动加锁。
   > - `@Log` / `@Slf4j` / `@Log4j` 等：用在类上，根据不同的注解生成不同类型的 log 对象。

6. **sql**查询优化？sql查询技巧与索引优化。

   > **sql**查询优化
   >
   > 1. 避免在 WHERE 子句中使用 `!=` 或 `<>` 操作符，否则将引擎放弃使用索引而进行全表扫描。
   >
   > 2. 考虑在 WHERE 及 ORDER BY 涉及的列上建立索引。
   >
   > 3. 尽量避免在 WHERE 子句中对字段进行 NULL 值判断，否则将导致引擎放弃使用索引而进行全表扫描。
   >
   > 4. IN 和 NOT IN 也要慎用，如果是连续数值，可以用 BETWEEN 代替。如果是子查询，可以用 EXISTS 代替。
   >
   > 5. 应尽量避免在 WHERE 子句中对字段进行表达式操作。
   >
   > 6. 应尽量避免在 WHERE 子句中对字段进行函数操作。
        >
        >    总之就是让引擎尽量放弃全表扫描而使用索引扫描。
   >
   > 数据库索引优化
   >
   > 1. 为经常用于搜索、排序和分组的列建立索引。
   >
   > 2. 避免为经常更新的列建立索引。因为每次更新都会导致索引的重建，这会降低更新操作的性能。
   >
   > 3. 尽量使用前缀索引。
        >
        >    > ```sql
   >    > CREATE INDEX index_name
   >    > ON table_name (column_name(length));
   >    > ```

7. **springboot**项目如何部署？

8. **mybaits-plus**的**BaseMapper**接口与**IServixe**接口的不同以及相同点，两者的使用场景？

   > `IService`针对业务逻辑层的封装，需要指定DAO层类和对应的实体类，是在`BaseMapper`基础上的加强。
   >
   > `IService`提供批处理操作，而`BaseMapper`没有。
   >
   > > ```java
   > > List<Entity> entityList = ...; // 需要插入的记录列表
   > > boolean result = service.saveBatch(entityList);
   > > ```

9. **Git**相关概念学习以及语法使用？







 
