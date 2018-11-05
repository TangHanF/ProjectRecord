## mybatis一次执行多条SQL语句

1. 首先在数据库连接URL上加上`allowMultiQueries=true`，默认mysql是不支持一次执行多条SQL语句的。

```
jdbc:mysql://127.0.0.1:3306/test?useUnicode=true&characterEncoding=utf-8&allowMultiQueries=true1
```

2 .在delete节点中添加多条语句: 

```
  <delete id="deleteByPrimaryKey" parameterType="java.lang.Integer" >
    delete from music_favorite where id = #{id,jdbcType=INTEGER};
    delete from music_favorite_song where f_id = #{id,jdbcType=INTEGER};
  </delete>
```

> 注意多条语句之间用“;”分割开来

这可以用在mybatis的级联关系删除上,删除主表记录前，先删除关联表的记录，两条一起执行