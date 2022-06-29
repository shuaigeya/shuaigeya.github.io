---
title: shoka 食用手册
sticky: true
tags:
- hexo
categories:
- 软件安装
---
## shoka 主题安装和配置

shok主题安装：[请戳此](https://shoka.lostyu.me/computer-science/note/theme-shoka-doc/)
shoka依赖插件的安装和配置：[请戳此](https://shoka.lostyu.me/computer-science/note/theme-shoka-doc/dependents/)
shoka主题基本配置：[请戳此](https://shoka.lostyu.me/computer-science/note/theme-shoka-doc/config/)
shoka界面显示相关配置：[请戳此](https://shoka.lostyu.me/computer-science/note/theme-shoka-doc/display/)

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