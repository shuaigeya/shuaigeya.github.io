---
title: myBatis 面试题
date: 2022-06-29 12:27:11
tags:
    mybatis
categories:
- 面试题集
---
## MyBatis 缓存
 **缓存**：暂存一些数据，加快系统查询速度。
 
 **Mybatis缓存机制**：本质是一个**Map**,能保存一些数据。
 
 **一级缓存**：线程级别的缓存。也称本地缓存或**sqlSession**级别的缓存。（和数据库的一次会话就有一次一级缓存）
 
 **二级缓存**：全局范围的缓存。（除了当前线程和**SqlSession** 能用外，其他的都能用）

### 一级缓存
只要之前查询过的数据，**MyBatis**都会保存在缓存中，下次获取这些数据，都会直接在缓存中拿。

>  注：**SpringBoot + Mybatis 一级缓存会失效**。原因是经过Spring的处理，每次查询完成后，都会关闭**sqlSession**，而一级缓存是**sqlSession**级别的缓存。

#### 缓存失效的几种情况

 1. 不同的 **sqlSession** ，同一级的缓存。
 2. 同一个方法，不同的参数。
 3. 在同一个**sqlSession**期间执行过任何一次增删改操作。
 4. 手动清空了缓存。

### 二级缓存

> 二级缓存没有，就去看一级缓存，一级缓存没有，就去读数据库。
> 关闭 **sqlSession** 会把一级缓存数据放在二级缓存中。

## MyBatis 动态标签
> **if、where、trim、set、foreach、collection、choose、sql、include、bing**

### if : 类似java中单分支  if  判断
```xml
 SELECT
	*
 FROM
 	tbl_navigation a
 WHERE
	<if test="obj.navigationId!=null and obj.navigationId!=''">
	    a.column_type = #{obj.navigationId}
	</if>
	<if test="obj.id!=null and obj.id!=''">
	    a.column_type = #{obj.id}
	</if>
```
### choose、when、otherwise 

>  **类似Java 的 if-else。**
>  1.当title 不为空， 选择title。
>  2.当content 不为空，title为空，选择content 。
>  3.当content 和 title 都为空，选择 otherwise。
>  4.当content 和 title 都为不为空，选择 title。

```xml
select * from tbl_column
<where>
      <choose >
          <when test="obj.title != null">
                 and title like #{obj.title}
          </when>
          <when test="content != null">
                 and content like #{obj.content}
          </when>
          <otherwise>
                 and delete = 1
          </otherwise>
     </choose>
</where>
```
### trim、where、set
> **where**: 替换sql语句中的where。只有当子元素有任何返回的情况，才会拼接 where。当子元素 以 or 或 and 开头 会去除。
>  **trim**: 可以去除 or 和and，在语句中拼接前缀或后缀。
> **set**: 替换sql语句中的set。动态在行首添加 set 删除子元素首行逗号。

### foreach

> 类似java 中的 foreach。
> **collection：collection**集合，可以为List,Set,Map。
> **item**： 每次遍历，index 对应的 对象。 
> **index**： 当前数组的下标
>  **open="(" separator="," close=")">** ：循环开始前加 '('，循环结束后加 ')'。循环过程中，每次循环结束后加，。

以下为官网案例：
```xml
<select id="selectPostIn" resultType="domain.blog.Post">
  SELECT *
  FROM POST P
  WHERE ID in
  <foreach item="item" index="index" collection="list"
      open="(" separator="," close=")">
        #{item}
  </foreach>
</select>
```
### 