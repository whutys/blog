---
title: myBatis
type: categories
copyright: true
date: 2019-01-10 19:48:50
categories: [java,javaweb]
tags: [mybatis,web后端框架]
---

动态sql

### if

```xml
<select id="queryByIdAndTitle"
     resultType="Blog">
  SELECT * FROM BLOG 
  WHERE 1=1 
  <if test="id!= null and title!=null">
    AND id=#{id} and title=#{title}
  </if>
</select>
```

### choose(when,otherwise)

```xml
<select id="queryBy"
     resultType="Blog">
  SELECT * FROM BLOG WHERE 1=1
  <choose>
    <when test="title != null">
      AND title like #{title}
    </when>
    <otherwise>
      AND id= 1
    </otherwise>
  </choose>
</select>
```

### where

```xml
<select id="queryBy" resultType="com.scme.pojo.User" parameterType="com.scme.pojo.User">
       select * from user 
       <where>
       <if test="username!=null and password!=null">
            and username=#{username} and password=#{password}
        </if>
       </where>
</select>
```

### trim where

```xml
<select id="queryBy" resultType="com.scme.pojo.User" parameterType="com.scme.pojo.User">
        select * from user 
        <trim prefix="WHERE" prefixOverrides="AND |OR ">
              <if test="username!=null and password!=null">
                  and username=#{username} and password=#{password}
              </if>
         </trim>
</select>
```

### set

```xml
<update id="updateUser" parameterType="com.scme.pojo.User">
        update user 
        <set>
             <if test="username!=null">
                      username=#{username}
             </if>
        </set>
        <where> 
             <if test="id!=null">
                     id=#{id}
             </if>
         </where>
</update>
```

### trim set

```xml
<update id="updateUser" parameterType="com.scme.pojo.User">
        update user 
 　　　　<trim prefix="set" prefixOverrides=",">
　　　　　　　　<if test="username!=null"> username=#{username} </if> 
　　　　 </trim>
 　　　 <where>
　　　　　　　　<if test="id!=null"> id=#{id} </if>
　　　　</where>
 </update>
```

### foreach

```xml
<delete id="batchDelete" parameterType="java.lang.String">
  delete from user
  where id in
  <foreach item="id" index="index" collection="list"
      open="(" separator="," close=")">
        #{id}
  </foreach>
</delete >
```

### bind创建变量

```xml
<select id="selectBlogsLike" resultType="Blog">
  <bind name="pattern" value="'%' + _parameter.getTitle() + '%'" />
  SELECT * FROM BLOG
  WHERE title LIKE #{pattern}
</select>
```

### include

```xml
<sql id="sqlref"></sql>
<select id="" parameterType="" resultMap="">
	<include refid="sqlref"/>
    ...
</select>
```



### 注解

```java
public interface ObjectMapper{
    //避免使用重载方法
    //静态sql
	@insert("insert into tablename(field1,...) values(#{param1},...)")
	void insertMethod(JavaObject javaObject);
	@delete("delete from tablename where field1=#{param1},...")
	void deleteMethod(JavaObject javaObject);
	@update("update tablename set field1=#{param1},...")
	void uodateMethod(JavaObject javaObject);
	@select("select field1,... from tablename where field1=#{param1},...")
	void selectMethod(JavaObject javaObject);
    //动态sql方法
    @insertProvider(type="SQL方法类路径",method="返回SQL语句的方法名")
	void insertMethod2(JavaObject javaObject);
	@deleteProvider(type="SQL方法类路径",method="返回SQL语句的方法名")
	void deleteMethod2(JavaObject javaObject);
	@updateProvider(type="SQL方法类路径",method="返回SQL语句的方法名")
	void uodateMethod2(JavaObject javaObject);
	@selectProvider(type="SQL方法类路径",method="返回SQL语句的方法名")
	void selectMethod2(JavaObject javaObject);
}
```

