# 1.简介

## 1.1、MyBatis是什么？

<img src="https://img-blog.csdnimg.cn/86d3fc960e394ea581c298332a0d590b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_20,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:80%;" />



## 1.2、MyBatis依赖

MyBatis是外国佬的啊，MyBatisPlus才是国人的。去Maven仓库找，即

```xml
<!-- https://mvnrepository.com/artifact/org.mybatis/mybatis -->
<dependency>
    <groupId>org.mybatis</groupId>
    <artifactId>mybatis</artifactId>
    <version>3.5.6</version>
</dependency>
```



## 1.3、什么是持久化、持久层？

因为数据在内存断电即失，肯定要持久化。

持久层：Dao层，Service层，Controller层等，完成持久化工作的代码块，层界限十分明显。



#  2、第一个MyBatis

## 2.1、准备数据库数据

```sql
CREATE DATABASE `mybatis`;

USE `mybatis`;

CREATE TABLE `user`(
`id` INT(20) NOT NULL PRIMARY KEY,
`name` VARCHAR(30) DEFAULT NULL,
`pwd` VARCHAR(30) DEFAULT NULL
)ENGINE=INNODB DEFAULT CHARSET=utf8;

INSERT INTO `user`(`id`,`name`,`pwd`) VALUES
(1,'肥莫1','1234'),
(2,'肥莫2','1234'),
(3,'肥莫3','1234')
```



## 2.2、创建空Maven+依赖导入

① 空 Maven

<img src="https://img-blog.csdnimg.cn/c74b1aa7100b4894a7b9f5befe8fdcff.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_19,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:67%;" />

②文件路径选择！

![img](https://img-blog.csdnimg.cn/8900323c72d4407ea4470efb218972a1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_9,color_FFFFFF,t_70,g_se,x_16)

③删除src目录

④pom中导入依赖

mysql、mybatis、junit都在Maven里面找！

```XML
    <dependencies>
    <!-- mybatis -->
        <dependency>
            <groupId>org.mybatis</groupId>
            <artifactId>mybatis</artifactId>
            <version>3.5.6</version>
        </dependency>
        <!--mysql驱动依赖-->
        <dependency>
            <groupId>mysql</groupId>
            <artifactId>mysql-connector-java</artifactId>
            <version>8.0.21</version>
        </dependency>
        <!--junit测试-->
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.11</version>
        <scope>test</scope>
    </dependency>
    </dependencies>
```



##  2.3、创建子模块

好处：大项目里可以创建许多个子项目，不用每次不同 测试都要重新导入依赖

![img](https://img-blog.csdnimg.cn/8f362ba1de414283bde160f5f4b6c77b.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_16,color_FFFFFF,t_70,g_se,x_16)

 子项目命名：

![img](https://img-blog.csdnimg.cn/abe807a72d6445e1805d33a8629856e3.png)

父工程下就多了个子模块

![img](https://img-blog.csdnimg.cn/776ce1b5cef74f9da11a42bb193c8410.png)

## 2.4、创建核心配置文件mybatis-config.xml

如下创建，在子模块的`resource`中创建该文件`mybatis-config.xml`

![img](https://img-blog.csdnimg.cn/143803ad754142cdb1eb55e816637777.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_13,color_FFFFFF,t_70,g_se,x_16)

在[Mybatis中文文档](https://mybatis.net.cn/getting-started.html)的入门中找到核心配置文件的代码添加到其中。

<img src="https://img-blog.csdnimg.cn/8fca1e57ff0b49fa9dd8c0fe15c69637.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_19,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom: 67%;" />

进行修改连接到各个创建的数据库！

<img src="https://img-blog.csdnimg.cn/56689a4f83254600928dda3a8bb51afd.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_20,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:67%;" />

代码如下：

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>
    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC"/>
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/mybatis?useSSL=true&amp;useUnicode=true&amp;characterEncoding=UTF-8"/>
                <property name="username" value="root"/>
                <property name="password" value="123456"/>
            </dataSource>
        </environment>
    </environments>
<!--    每一个Mapper.xml都得在核心配置文件中注册-->
    <mappers>
        <mapper resource="com/cola/dao/UserMapper.xml"/>
    </mappers>
</configuration>
```



## 2.5、编写mybatis的工具类

> mybatis的工具类的作用：[mybatis工具类及其使用](https://blog.csdn.net/wx5040257/article/details/78726291)；

在main下的java下创建`com.cola.Utils`包

创建`mybatisUtils.java`代码如下

```java
//SqlSessionFactory->SqlSession
public class MybatisUtils {
    private static SqlSessionFactory sqlSessionFactory;

    static {
        try {
// 使用Mybatis第一步:获取sqLSessionFactory对象
            String resource = "mybatis-config.xml";
            InputStream inputStream = Resources.getResourceAsStream(resource);
            sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

//有了SqlSessionFactory，就有了SqlSession示例，SqlSession就有sql的语句了
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession();
    }
}
```



##  2.6、编写接口和实现类 

:one:先创建好实体类pojo！

---

:two:编写接口interface

`List<User> getUserList`，即返回结果为List集合

![img](https://img-blog.csdnimg.cn/ad6f9e15817449ba8b4cdc2e1c5dd2e8.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_11,color_FFFFFF,t_70,g_se,x_16)

---

:three:接口实现类Mapper

> namespace：绑定你指定的接口
>
> resultType：查询出的字段直接与pojo的字段映射。如果SQL返回的是int型，那么resultType定义成int型即可直接与Java进行绑定（基本数据类型默认可不写）。        resultType对应的是java对象中的属性，大小写不敏感。**使用了resultType进行对象赋值时，对象字段会与SQL查询中的字段对应，不对应就会被置null**。只需要将SQL中的字段别名设置与实体对象的字段名一致即可，当然也可以使用resultMap自定义设置字段对应。
>
> resultMap：如果是返回一个复杂的对象，就可以使用resultMap。resultMap可以对返回的参数进行配置，mybatis默认会进行驼峰转换。
>
> 
>
> 总结：查询进行select映射的时候，返回类型可以用resultType，也可以用resultMap。resultType是直接表示返回类型的，而resultMap则是对外部ResultMap的引用，但是resultType跟resultMap不能同时存在。在MyBatis进行查询映射时，其实查询出来的每一个属性都是放在一个对应的Map里面的，其中键是属性名，值则是其对应的值。
> ①==其实MyBatis的每一个查询映射的返回类型都是ResultMap==，当提供的返回类型==属性是resultType的时候，MyBatis会自动把对应的值赋给resultType所指定对象的属性==。
> ②当提供的返回类型是resultMap时，因为Map不能很好表示领域模型，就需要自己再进一步的把它转化为对应的对象，这常常==在复杂查询中很有作用==。
>
> 原文链接：https://blog.csdn.net/xushiyu1996818/article/details/89075069



![img](https://img-blog.csdnimg.cn/ac5cd1c94a2943828843f35a56ecdf4c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_15,color_FFFFFF,t_70,g_se,x_16)

select标签id相当于实现类==重写了接口的方法==！

重写了方法 ，还要有返回结果，一个是集合resultMap，一个是结果resultType：后面填写的就是映射他们的路径实体类的User！

![img](https://img-blog.csdnimg.cn/bdf4162c0a5f49b9a1804b888a95df12.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_6,color_FFFFFF,t_70,g_se,x_16)



```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--        namespace绑定了dao/Mapper接口-->
<mapper namespace="com.cola.dao.Userdao">
    <select id="getUserList" resultType="com.cola.pojo.User">
    select * from mybatis.user
  </select>
</mapper>
```





##  2.7、测试

测试在绿色的java文件中建包，与源代码模块一一对应，com.cola.dao

![img](https://img-blog.csdnimg.cn/c32b0035ec0a463d89a2544b106157a7.png)

创建UserdaoTest.java进行测试。

拿到对象自然可以操作起来！

**拿到连接数据库的SqlSession对象→拿到Userdao的class实例化的操作对象→直接使用他里边的方法！**

```java
public class UserdaoTest {
    @Test
    public void test(){
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        Userdao userdao = sqlSession.getMapper(Userdao.class);
        List<User> userList = userdao.getUserList();

        for (User user : userList) {
            System.out.println(user);

        }
//        关闭sqlSession
        sqlSession.close();
    }
}
```



## 2.8、Maven资源，target中xml文件无法生成

一般运行[maven](https://so.csdn.net/so/search?q=maven&spm=1001.2101.3001.7020)项目时，发现生成的target目录下，缺少原项目下的java或者resource的一些xml文件。

![img](https://img-blog.csdnimg.cn/f64ac5ad84ea415ba956bbf7db18ab42.png)



可以在maven依赖pom文件下做如下配置:（针对java和resources两个目录）

```XML
 <build>
        <resources>
            <resource>
                <directory>src/main/java</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
            <resource>
                <directory>src/main/resources</directory>
                <includes>
                    <include>**/*.properties</include>
                    <include>**/*.xml</include>
                </includes>
                <filtering>false</filtering>
            </resource>
        </resources>
    </build>
```



# 3、常见SQL语句示例 

## 3.1、基本增删改查

①编写接口

```java
public interface UserMapper {
    List<User> getUserList();
//    根据id查询
    User getById(int id);
//    create
    int addUser(User user);
//    update
    int updateUser(User user);
//    delete
    int deleteUser(int id);
}
```



②编写Mapper.xml

```XML
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<!--        namespace绑定了dao/Mapper接口-->
<mapper namespace="com.cola.dao.UserMapper">
    
    <select id="getUserList" resultType="com.cola.pojo.User">
        select * from mybatis.user
    </select>
    
    <!--  parameterType：传入的参数类型-->
    <select id="getById" parameterType="int" resultType="com.cola.pojo.User">
        select * from mybatis.user where id=#{id}
    </select>
    
     <!--  parameterType：传入的参数类型-->
    <insert id="addUser" parameterType="com.cola.pojo.User">
         insert into mybatis.user (id,name,pwd) values(#{id},#{name},#{pwd})
    </insert>
    
     <!--  parameterType：传入的参数类型-->
    <update id="updateUser" parameterType="com.cola.pojo.User">
         update mybatis.user set name=#{name}, pwd=#{pwd} where id=#{id};
  </update>
    
    <delete id="deleteUser" parameterType="int">
         delete from mybatis.user where id=#{id};
  </delete>
</mapper>
```



③测试：增删改查【  增删改要提交事务 sqlSession.commit();  】

```java
public class UserdaoTest {
    @Test
    public void test(){
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper userMapper = sqlSession.getMapper(UserMapper.class);
        List<User> userList = userMapper.getUserList();

        for (User user : userList) {
            System.out.println(user);

        }
//        关闭sqlSession
        sqlSession.close();
    }

    @Test
    public void getById(){
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getById(1);

            System.out.println(user);


//        关闭sqlSession
        sqlSession.close();
    }

    @Test
    public void addUser(){
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.addUser(new User(4, "肥莫4", "123456"));
//        增删改都要提交事务
        sqlSession.commit();

//        关闭sqlSession
        sqlSession.close();
    }
    @Test
    public void updateUser(){
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.updateUser(new User(1, "改了肥莫1", "123456"));
//        增删改都要提交事务
        sqlSession.commit();

//        关闭sqlSession
        sqlSession.close();
    }
    @Test
    public void deleteUser(){
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.deleteUser(4);
//        增删改都要提交事务
        sqlSession.commit();

//        关闭sqlSession
        sqlSession.close();
    }
}
```



## 3.2、Map集合作为参数，实现表的局部更新

①接口：看`addUser2`方法

![img](https://img-blog.csdnimg.cn/722b8d86df864413abef16b1041a27d1.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_7,color_FFFFFF,t_70,g_se,x_16)

 ②实现类：可以发现，添加用户我可以仅仅添加id和name而没有pwd，这就是map集合的万能局部字段更新！

![img](https://img-blog.csdnimg.cn/59dcbb0e8a3540979468bb4b0a70679d.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_10,color_FFFFFF,t_70,g_se,x_16)

③测试：仅仅添加id和名字到数据库

![img](https://img-blog.csdnimg.cn/af238ae2578b42898d975e2bf2b4cd1c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_11,color_FFFFFF,t_70,g_se,x_16)

##  3.3、模糊查询示例

接口

![img](https://img-blog.csdnimg.cn/c537ad4bdc4d48eb98485b9c27f7b1ed.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_11,color_FFFFFF,t_70,g_se,x_16)

实现

![img](https://img-blog.csdnimg.cn/4f826291e0a3452cb6f37cc4a291132c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_13,color_FFFFFF,t_70,g_se,x_16)

 测试：模糊查询所有姓李的人

![img](https://img-blog.csdnimg.cn/18ad0432bbe74d03a51d3e0a1b4062c7.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_14,color_FFFFFF,t_70,g_se,x_16)





## 3.4、limit实现分页

接口

```java
//    limit
    List<User> getUserByLimit(Map<String,Integer> map);
```



实现类

```XML
    <select id="getUserByLimit" parameterType="map" resultType="com.cola.pojo.User">
        select * from mybatis.user limit #{startIndex},#{pagesize}
    </select>
```



测试

```java
    @Test
    public void getUserByLimit(){
        //        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        HashMap<String, Integer> map = new HashMap<String, Integer>();
        map.put("startIndex",1);
        map.put("pagesize",2);

        List<User> userList = mapper.getUserByLimit(map);
        for (User user : userList) {
            System.out.println(user);
        }
//        关闭sqlSession
        sqlSession.close();
    }
}
```









#  4、多数据库源&ResultType别名&xml文件映射

## 4.1、mybatis-config.xml多环境

### 1、方式①：直接配置多数据库源

mybatis-config.xml中可以配置多个数据库源，但只能选择其中一个！

如图，增加了**test**的环境。

![img](https://img-blog.csdnimg.cn/31f6ae95226c4306a27c6fc562630433.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_12,color_FFFFFF,t_70,g_se,x_16)

 Mybatis默认的==事务管理就是JDBC，连接池是POOLED==，如上图。

### 2、方式②：使用db.properties文件

将连接数据库的信息写到这里

<img src="https://img-blog.csdnimg.cn/3e348a9f3a1b4308ae57851f235d4a5e.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_17,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:80%;" />

然后把db.properties引进xml文件，注意有顺序！properties必须在前面

environment那里就不用写死了

![img](https://img-blog.csdnimg.cn/596854e0df094db780874848c341c661.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_15,color_FFFFFF,t_70,g_se,x_16)



---

此外，如果数据库源有些字段没有写，可以这样写上去，如果你写的字段外部有了，会与外部的为主

<img src="https://i0.hdslb.com/bfs/album/b74125529792b8b1d93a757992a763834efb1e64.png" alt="image-20220623122912910" style="zoom:80%;" />

---







## 4.2、在核心配置文件中对resultType起别名

> 目的：把resultType的`com.cola.pojo.User` 名字用`User`代替

### 方式1：直接起别名

在`mybaitis-config.xml`中，使用==改名的方法起别名==，改为`User`了

![img](https://img-blog.csdnimg.cn/238f576e824b4db28335de8ce6ee7f0c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_12,color_FFFFFF,t_70,g_se,x_16)

### 方式2：直接声明包名前缀

或者不改名，直接==先声明好包名==也是一样的效果：

![img](https://img-blog.csdnimg.cn/22a89ac8ff4d4e7fa493e0a1324c5f95.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_9,color_FFFFFF,t_70,g_se,x_16)

用了方式2后，也可以在**实体类直接加注解@Alias来起别名，随便起名，图中user，也可以cola。**

![img](https://img-blog.csdnimg.cn/e9a8117c03864cf68529bd1d5971ab7f.png)



> 一般都选方式2，直接声明好包名完事。

实体类少，我就第①种改名的；还可以自定义名字，一举两得；

实体类多，我就第②种直接声明咯，直接什么好包名就一本万利。想自定义名字可以@Alias（“自定义”）



## 4.3、resultType和resultMap的区别

- resultType：查询出的字段直接与pojo的字段映射。如果SQL返回的是int型，那么resultType定义成int型即可直接与Java进行绑定（基本数据类型默认可不写）resultType对应的是java对象中的属性，大小写不敏感。使用了resultType进行对象赋值时，对象字段与SQL查询中的字段对应，就会被置null。只需要将SQL中的字段别名设置与实体对象的字段名一致即可，当然也可以使用resultMap自定义设置字段对应。
- resultMap：如果是返回一个复杂的对象，属性和数据库的不一致，多表查询之类。就可以使用resultMap。resultMap可以对返回的参数进行配置，mybatis默认会进行驼峰转换。


> 总结：查询进行select映射的时候，返回类型可以用resultType，也可以用resultMap。resultType是直接表示返回类型的，而resultMap则是对外部ResultMap的引用，但是resultType跟resultMap不能同时存在。在MyBatis进行查询映射时，其实查询出来的每一个属性都是放在一个对应的Map里面的，其中键是属性名，值则是其对应的值。
> ①==其实MyBatis的每一个查询映射的返回类型都是ResultMap==，当提供的返回类型==属性是resultType的时候，MyBatis会自动把对应的值赋给resultType所指定对象的属性==。
> ②当提供的返回类型是resultMap时，因为Map不能很好表示领域模型，就需要自己再进一步的把它转化为对应的对象，这常常==在复杂查询中很有作用==。

原文链接：https://blog.csdn.net/xushiyu1996818/article/details/89075069



##  4.4、mapper.xml文件需注册

**mapper.xml**：即接口实现类，**具体的SQL语句都写在xml文件**！

**目的**：每一个`Mapper.xml`，都要在核心配置文件mybatis-config.xml中注册。

有三种方式注册：resource、class、name。



> 注意：
>
> 方式1好用：路径、包名直接指定，不会出错。
>
> 方式2和方式3：接口mapper和mapper.xml必须同名，而且需在同一个dao包下。

<img src="https://i0.hdslb.com/bfs/album/3ff5394dc29d625add069b3fac91039c94755802.png" alt="image-20220623124220363" style="zoom:67%;" />

---

<img src="https://img-blog.csdnimg.cn/7bfaa8f8194b494f85afa40c1dc92d47.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_14,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:80%;" />

---





# 5、生命周期和作用域（未完成）

生命周期即这个东西要存在多久？

作用域就是局部变量还是全局？

![img](https://img-blog.csdnimg.cn/f4e4a365d5a84463a622d77ba429adea.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_19,color_FFFFFF,t_70,g_se,x_16)



# 6、解决Java属性名和sql字段名不一致

如图：定义的实体类名和数据库名不同

![img](https://img-blog.csdnimg.cn/24f30f35f43c49518b0b802ee44275cb.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_12,color_FFFFFF,t_70,g_se,x_16)

 在实现类编写查询语句时候，查询出的password为空，因为从数据库查出来的字段叫是pwd，无法映射给实体类的password，当然为null。

### 方式1：在SQL语句中起别名

把从数据库查出来的pwd，又命名为password，这样就映射得上实体类了。

![img](https://img-blog.csdnimg.cn/e80aff4694c848349f4ed8b9d9457a92.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_19,color_FFFFFF,t_70,g_se,x_16)

### 方式2：ResultMap结果集映射

在实现类xml文件如下设置！

![img](https://img-blog.csdnimg.cn/6c1298c50ae042bf8e2b9e31631c0752.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_16,color_FFFFFF,t_70,g_se,x_16)





#  7、日志工厂

> **作用：**数据库操作出现了异常，我们需要排错，日志工厂就是做好的助手

**为什么不用sout？**

1. 我们之前看到`log4j`的配置文件中有输出到文件的相关配置，查找日志信息的时候，可以到相应的日志文件中去查看，如果是sout的话，程序关闭，信息就丢失
2. 最关键的是**sout是系统运行级别，影响程序性能十分夸张！**





## 7.1、最简单示例

如何添加日志工厂？

> 在mybatis-config.xml中添加：注意xml文件标签有顺序要求，settings标签图位置较为靠前

STDOUT_LOGGING只是其中一种类型

![img](https://img-blog.csdnimg.cn/73ccf657eeb04f23ace8158c5c41d91a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_12,color_FFFFFF,t_70,g_se,x_16)

---

其他类型：logImpl

> SLF4J | LOG4J | LOG4J2 | JDK_LOGGING | COMMONS_LOGGING | `STDOUT_LOGGING` | NO_LOGGING

![img](https://img-blog.csdnimg.cn/29e9e71d96a34025879eb9c5043cd77a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_20,color_FFFFFF,t_70,g_se,x_16)



---

**输出结果：**

![img](https://img-blog.csdnimg.cn/1a8aa6694eed480ebc668924ffa75a0c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_14,color_FFFFFF,t_70,g_se,x_16)

---





## 7.2、添加Log4j日志

### 1、导入Log4j的依赖

```XML
<!-- https://mvnrepository.com/artifact/log4j/log4j -->
<dependency>
    <groupId>log4j</groupId>
    <artifactId>log4j</artifactId>
    <version>1.2.17</version>
</dependency>
```

### 2、 创建Log4j.properties配置文件

```properties
#将等级为DEBUG的日志信息输出到console和file这两个目的地，console和file的定义在下面的代码
log4j.rootLogger=DEBUG,console,file

#控制台输出的相关设置
log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.Target = System.out
log4j.appender.console.Threshold=DEBUG
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=[%c]-%m%n

#文件输出的相关设置
log4j.appender.file = org.apache.log4j.RollingFileAppender
log4j.appender.file.File=./log/kuang.log
log4j.appender.file.MaxFileSize=10mb
log4j.appender.file.Threshold=DEBUG
log4j.appender.file.layout=org.apache.log4j.PatternLayout
log4j.appender.file.layout.ConversionPattern=[%p][%d{yy-MM-dd}][%c]%m%n

#日志输出级别
log4j.logger.org.mybatis=DEBUG
log4j.logger.java.sql=DEBUG
log4j.logger.java.sql.Statement=DEBUG
log4j.logger.java.sql.ResultSet=DEBUG
log4j.logger.java.sql.PreparedStatement=DEBUG
```



### 3、在核心配置文件注册

![img](https://img-blog.csdnimg.cn/6046b3c63ea64561813202b160157a86.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_14,color_FFFFFF,t_70,g_se,x_16)



### 4、测试使用

如果哪个java文件需要排错，就在那里导入Log4j包，然后创建实例化对象，最后使用即可！**

例如我要在测试类进行日志排错

![img](https://img-blog.csdnimg.cn/23cc81b8613b4f8586c3a19dd948eb01.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_12,color_FFFFFF,t_70,g_se,x_16)

### 5、日志级别：

<img src="https://img-blog.csdnimg.cn/6cd4d4e6954f4c95aa4a860b14f399de.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_17,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:80%;" />

log4j规定了默认的几个级别：trace<debug<info<warn<error<fatal

意思是如果你设置日志级别是trace，则大于等于这个级别的日志都会输出

 C：error 指出虽然发生错误事件，但仍然不影响系统的继续运行。
 D：warn 表明会出现潜在的错误情形。
 E：info 一般和在粗粒度级别上，强调应用程序的运行全程。
 F：debug 一般用于细粒度级别上，对调试应用程序非常有帮助。





# 8、使用注解开发

> 使用注解开发，可以不用写Mapper.xml文件，SQL语句直接写在接口mapper



## 8.1、注解写SQL演示

①mybatis-config.xml

核心配置文件注册改一下

![img](https://img-blog.csdnimg.cn/06b89ea3f5de4f7081124068a835d6d6.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_9,color_FFFFFF,t_70,g_se,x_16)

 ②接口演示：查询所有用户

```java
public interface UserMapper {
    @Select("select * from user")
    List<User> getUsers();
}
```



> 如果写传入参数的SQL呢？参数不止一个呢？那必须配合@Param注解了。看下文：



## 8.2、@Param()注解

**①为什么使用？**

在接口中不写@Param，在xml中就需对传入的参数需标明parameterType，仅仅一个参数时候可不写这个注解，mybatis可自动识别。



**②但是传入多个参数，xml文件的parameterType怎么标识？这时候，需要@Param()注解。**

> 当**使用了**@Param注解来声明参数的时候，不需标明parameterType，SQL取值就可以取到。且语句取值使用`#{}`，`${}`都可以。
>
> 当**不使用**@Param注解声明参数的时候，需标明parameterTypeSQL，必须使用的是#{}来取参数。使用${}方式取值会报错。
>
> 这个注解是**为SQL语句中参数赋值**而服务的。==多个参数时候，必须使用@Param==。

多个参数，必须加@Param即可，如下图所示

![img](https://img-blog.csdnimg.cn/9fe0b7bfdf3748a6b6df0954926d7918.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_15,color_FFFFFF,t_70,g_se,x_16)

---

此时，mapper.xml中，不用写parameterType了。

==重点是：SQL语句对应的形参对应的是@Param注解的形参==！

<img src="https://i0.hdslb.com/bfs/album/23e493137d5d3fb0d3590fb00f7db84976d58924.png" alt="image-20220623150900463" style="zoom: 80%;" />

---



 ②接口的方法和注解实现

```java
    @Select("select * from user where id=#{id}")
    User getUserByID(@Param("id") int id);
    @Insert("insert into user(id,name,pwd) values(#{id},#{name},#{password})")
    int addUser(User user);
    @Delete("delete from user where id=#{id}")
    int deleteUser(@Param("id") int id);
```



③工具类自动提交事务

```java
    //有了SqlSessionFactory，就有了SqlSession示例，SqlSession就有sql的语句了
    public static SqlSession getSqlSession(){
        return sqlSessionFactory.openSession(true);//填了true就会自动提交事务！
    }
```



④测试增删改查

```java
    @Test
    public void test02(){
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getUserByID(1);
        System.out.println(user);
//        关闭sqlSession
       sqlSession.close();
    }

    @Test
    public void test03() {
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.addUser(new User(6, "肥莫6", "12345"));
//        关闭sqlSession
        sqlSession.close();
    }

    @Test
    public void test04() {
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.deleteUser(5);
//        关闭sqlSession
        sqlSession.close();
    }

    @Test
    public void test05() {
//        1.获取SqlSession对象
        SqlSession sqlSession = MybatisUtils.getSqlSession();
//        从Mapper获取
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        mapper.updateUser(new User(3,"改肥莫","00000"));
//        关闭sqlSession
        sqlSession.close();
    }
```



# 9、Lombok的使用

①在idea下载Lombok插件

②在Maven导入依赖

③@Data@No （无参）@All... （全参）等等在实体类加注解节省工作！





# 10、多对一：多表查询

> **对象用association：多对一**
>
> **集合用collection ：一对多**

## ①准备工作

数据库表如下：

![img](https://img-blog.csdnimg.cn/8e62351c4b1f4fc39b6700f5561742a4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_4,color_FFFFFF,t_70,g_se,x_16)

---

建实体类

![img](https://img-blog.csdnimg.cn/63386b5fd20045eab0824e167bd1f1e0.png)

---

创建Mapper接口

![img](https://img-blog.csdnimg.cn/2b51464a33b5467498dfe335c29b9537.png)

---

创建Mapper.xml

![img](https://img-blog.csdnimg.cn/a0be9907762a4713b9c9cb93f03e2b56.png)

---


在核心配置文件中，注册xml文件。



## ②多表查询

> **问题**：查询每个学生对应的老师是谁，要进行多对一处理



### 方式1：子查询（难理解）

进行结果映射集，学生类的tid映射到老师的查询，用法如图

![img](https://img-blog.csdnimg.cn/22c24c01ba56493394f34edb4595acd4.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_14,color_FFFFFF,t_70,g_se,x_16)

**对象用association：多对一**

**集合用collection ：一对多**

> select="getTeacher"				说明用了一个select语句是getTeacher     
>
> javaType="Teacher" 				JavaType即对应学生类的private Teacher teacher；这个数据Teacher就用
>
>  ofType="Student"  				 是集合的泛型类型，即对应老师实体类里的泛型属性`private List<Student> student;`

```XML
    <select id="getStudent" resultMap="StudentTeacher">
        select * from student
    </select>
    
    <resultMap id="StudentTeacher" type="Student">
<!--        property="teacher"是学生实体类的那个private Teacher teacher；-->
        <association property="teacher" column="tid" javaType="Teacher" select="getTeacher"/>
    </resultMap>

    <select id="getTeacher" resultType="Teacher">
<!-- tid形参随便填的-->
        select * from teacher where id=#{tid}
    </select>
```



### 方式2：联表查询（好理解）

![img](https://img-blog.csdnimg.cn/be7ca435442248f0bb04ef3c5dbbbffe.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_12,color_FFFFFF,t_70,g_se,x_16)

# 11、一对多：多表查询

> **对象用association：多对一**
>
> **集合用collection ：一对多**

**一个老师对应多个学生**，老师的实体类这样写：

```
private List<Student> students;
```

xml文件

方式一：联表查询

```XML
    <select id="getTeacher" resultMap="TeacherStudent">
        select s.id sid,s.name sname,t.name tname,t.id tid
        from student s,teacher t
        where s.tid=t.id and t.id=#{tid}
    </select>

    <resultMap id="TeacherStudent" type="Teacher">
        <result property="id" column="tid"/>
        <result property="name" column="tname"/>
<!--        对于属性中的集合List<Student>要用collection-->
<!--        javaType 是属性的类型，比如多对一的老师、或者String name的String，或List集合的ArrayList-->
<!--        ofType  是集合的泛型类型-->
        <collection property="students" ofType="Student">
            <result property="id" column="sid"/>
            <result property="name" column="sname"/>
            <result property="tid" column="tid"/>
        </collection>
    </resultMap>
```



方式二：子查询

<img src="https://img-blog.csdnimg.cn/31c4fe31aae3496e93e12cb285629457.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_20,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:80%;" />

---

总结

<img src="https://img-blog.csdnimg.cn/38cf186ad57444fcbc3840e7f5e44381.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_17,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom:67%;" />

---



# 12、动态SQL（动态查询）

## ①环境准备

数据库创建好Blog表

工具类增加IDutils类，用于生成数据库的主键id，他可以生成不重复随即码。

```java
public class IDutils {
    public static String getId(){
        return UUID.randomUUID().toString().replace("-","");
    }

    @Test
    public void test(){
        System.out.println(IDutils.getId());
    }
}
```



## ②IF语句、when（if=when）

作用：拼接查询

- 可以随便按作者名字查询、标题查询等等，或者连接起来查询
- 查询“狂神”的“mybatis”课程，就要找到符合“狂神”和“mybatis”这两个的要求的查询，而不是满足其中一个就可以了

接口方法：

```java
List<Blog> queryBlogIF(Map map);
```



实现：where 1=1，如果什么都不查询，就会返回所有真结果。

```XML
<!--    动态查询-->
    <select id="queryBlogIF" parameterType="map" resultType="blog">
        select * from mybatis.blog where 1=1
        <if test="title!=null">
            and title=#{title}
        </if>
        <if test="author!=null">
            and author=#{author}
        </if>
    </select>


例子2：where的作用就是为了判断是否要去除and
<select id="selectOperLogList" parameterType="SysOperLog" resultMap="SysOperLogResult">
		<include refid="selectOperLogVo"/>
		<where>
			<if test="title != null and title != ''">
				AND title like concat('%', #{title}, '%')
			</if>
			<if test="businessType != null">
				AND business_type = #{businessType}
			</if>
		</where>
		order by oper_id desc
	</select>
```



测试方法：

```java
    @Test
    public void queryBlogIF(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        HashMap map = new HashMap();
        map.put("title","微服务");
        List<Blog> blogs = mapper.queryBlogIF(map);
        for (Blog blog : blogs) {
            System.out.println(blog);
        }
        sqlSession.close();
    }
```



## ③choose、where、set

> where标签作用：自动地判断我们SQL语句==是否需要增加、删除and、or==连接词

****

![img](https://img-blog.csdnimg.cn/342a904a847346da92b43a774a08dd00.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_13,color_FFFFFF,t_70,g_se,x_16)

> choose作用：选择查询，相当于Java的Switch，配合when、otherwise

**查询**实现：

```XML
 <select id="queryBlogChoose" parameterType="map" resultType="blog">
        select * from mybatis.blog
        <where>
            <choose>
                <when test="title!=null">
                    title=#{title}
                </when>
                <when test="author!=null">
                    author=#{author}
                </when>
                <otherwise>
                    and views=#{views}
                </otherwise>
           </choose>
       </where>
    </select>
```



测试：choose执行第一个符合条件的输出，如下图，只会输出一条微服务的数据！

![img](https://img-blog.csdnimg.cn/ce3627801d7346979c36501ef72d913d.png)

> set标签：==更新update就要用==，**自动删除逗号，来看是否只更新一部分**

根据id号更新数据库的实现：

```XML
    <update id="updateBlog" parameterType="map">
        update mybatis.blog
        <set>
            <if test="title!=null">
                title=#{title},
            </if>
            <if test="author!=null">
                author=#{author}
            </if>
        </set>
            where id=#{id}
    </update>
```



## ④SQL片段-代码复用

**作用**：把每个sql语句都用到的公共代码提取出来，复用！

**提取**：直接在实现类。用上sql标签

```XML
    <sql id="if-title-author">
        <if test="title!=null">
            title=#{title},
        </if>
        <if test="author!=null">
            author=#{author}
        </if>
    </sql>
```



使用：在更新数据上使用，用include标签

```XML
    <update id="updateBlog" parameterType="map">
        update mybatis.blog
        <set>
            <include refid="if-title-author"></include>
        </set>
            where id=#{id}
    </update>
```



**注意：**sql标签语句内，不要有where和set！因为他们会自动删除and，逗号

## ⑤Foreach循环修改数据库

**使用示例**：查询id为1,2,3的数据；

collection是id号的集合、item就是传参的id、open是语句开始的符号（、close是结尾的符号）、

separator是语句中间的or。

![img](https://img-blog.csdnimg.cn/f84c884feb154103a593b05ffc6f6c1a.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-v5LmQ5paw5omLaGVsbG8gd29ybGQ=,size_18,color_FFFFFF,t_70,g_se,x_16)

 比如：我要一次性删除数据库中id为5-8号的用户；

```XML
    <delete id="deleteBlog" parameterType="map">
        delete from mybatis.blog
        <where>
            <foreach collection="ids" item="id" open="(" close=")" separator="or">
                id=#{id}
            </foreach>
        </where>
    </delete>


若依框架例子2：
	<delete id="deleteOperLogByIds" parameterType="Long">
 		delete from sys_oper_log where oper_id in
 		<foreach collection="array" item="operId" open="(" separator="," close=")">
 			#{operId}
        </foreach> 
 	</delete>
```



测试：

```java
    @Test
    public void deleteBlog(){
        SqlSession sqlSession = MybatisUtils.getSqlSession();
        BlogMapper mapper = sqlSession.getMapper(BlogMapper.class);
        HashMap map = new HashMap();
//创建整数集合，把id号添加到里面，再把他放入map集合；
        ArrayList<Integer> ids = new ArrayList<Integer>();
        ids.add(5);
        ids.add(6);
        ids.add(7);
        ids.add(8);
        map.put("ids",ids);
        mapper.deleteBlog(map);
        sqlSession.close();
    }
```



# 13、mybatis的缓存

## ①缓存介绍

用户读取数据，过程经过是：用户→服务器→数据库

用户数多了，会有并发问题，这时候，在服务器与数据库间插入一个缓存服务器来解决。

**作用：**

> 1.什么是缓存[ Cache ]?

- 存在内存中的临时数据。
- 将用户经常查询的数据放在缓存(内存)中，用户去查询数据就不用从磁盘上(关系型数据库数据文件)查询，从缓存中查询，从而提高查询效率，解决了高并发系统的性能问题。

> 2.为什么使用缓存?

- 减少和数据库的交互次数，减少系统开销，提高系统效率。 

> 3.什么样的数据能使用缓存?

- 经常**查询**并且不经常改变的数据。



​        二级缓存nameSpace，全局缓存才有用！



## ②一级缓存测试

> **mybatis的一级缓存sqlSession，仅仅是一个会话作用域缓存**。
>
> 一级缓存只在sqlSession开启---关闭之间有效。因此，mybatis**默认开启的**就是一级缓存

想查看效果，首先要开启日志，在用sql根据id查询同一个用户**两次**的时候，数据库只会查询**一次**，因为sqlSession是**一级缓存**（



但是在这两次查询之间的代码，插入一个增删改操作，则这两个查询操作会执行两次，如下图所示：

因为**增删改有数据变动。会使缓存刷新！**   或者**手动清理缓存（如下代码），**也会查询两次。

```java
SQLSession.clearCache();
```



<img src="https://img-blog.csdnimg.cn/76d17ebc728a424daa0c74541544b816.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-25LiK6JCn,size_20,color_FFFFFF,t_70,g_se,x_16" alt="img" style="zoom: 80%;" />

## ③二级缓存测试

**原理作用：**

- 一个会话查询一条数据，这个数据就会被放在当前会话的一级缓存中;
- 如果当前会话关闭了，这个会话对应的一级缓存就没了；但是我们想要的是，会话关闭了，一级缓存中的数据被保存到二级缓存中;（**也就是说：一级缓存被close关闭了，二级缓存才生效**）
- 新的会话**查询**信息，就可以从二级缓存中获取内容;（所以**只能“查询”的放缓存**）
- 不同的mapper查出的数据会放在自己对应的缓存(map）中;
  

**1.实体类开启序列化：**为什么呢？

`<cache/>`中的readOnly默认为false，而可读写的缓存会通过序列化返回缓存对象的拷贝，此时需要**实体类**（这里是User）实现**Serializable接口**或者配置readOnly=true 

![img](https://img-blog.csdnimg.cn/7abd00601c7a4e33b6ca2f8d786eb7ab.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-25LiK6JCn,size_20,color_FFFFFF,t_70,g_se,x_16)

**2.开启二级缓存：**在mybatis-config文件中开启

```XML
    <settings>
<!--        开启Log4j日志-->
        <setting name="logImpl" value="Log4j"/>
<!--        开启二级缓存-->
        <setting name="cacheEnabled" value="true"/>
    </settings>
```



3.**在Mapper.xml文件中**使用：

```XML
<!--    默认配置缓存-->
    <cache/>
    <!--    高级的定义配置缓存-->
    <cache
            eviction="FIFO"
            flushInterval="60000"
            size="512"
            readOnly="true"/>
```



4.**某条语句不想放缓存里**，因为他更新太频繁

![img](https://img-blog.csdnimg.cn/bd257e1c6ebb47d4b022ed1a464e33fa.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-25LiK6JCn,size_20,color_FFFFFF,t_70,g_se,x_16)

**5.总结：**

- 只要开启了二级缓存，在同一个Mapper下就有效所有的数据都会先放在一级缓存中;
- 只有当会话提交，或者关闭的时候，才会提交到二级缓冲中!
  

**执行原理** 

**缓存顺序**

- **1.先看二级缓存中有没有**
- **2.再看一级缓存中有没有**
- **3.查询数据库**
  

 ![img](https://img-blog.csdnimg.cn/f9c3205098c540b89194ebdb40284707.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBA5Y-25LiK6JCn,size_20,color_FFFFFF,t_70,g_se,x_16)



## ④自定义缓存

没啥用，redis才是神！



更多知识参考菜鸟教程





# 完结撒花

# 

#  