## 前言

在实际开发中会遇到这种情况，就是一条数据需要判断是新增还是更新，正常的开发思路是先去查询这条数据的Id是否已经存在于数据库，存在就是update，否则为insert，mybatis也是基于这样的思想实现的，下面就举个例子看一下。

## 具体实现

比如，前台将一条教师的信息保存到教师的实体bean中，然后需要将这条信息保存到数据库中，这时需要判断一下教师信息是要update还是insert。 
教师信息实体bean如下：Teacher.java

```java
public class Teacher {

    private int teacherId;//教师Id

    private String teacherName;//教师名

    private int count;//mybatis判断Id是否存在

    public int getTeacherId() {
        return teacherId;
    }

    public void setTeacherId(int teacherId) {
        this.teacherId = teacherId;
    }

    public String getTeacherName() {
        return teacherName;
    }

    public void setTeacherName(String teacherName) {
        this.teacherName = teacherName;
    }

    public int getCount() {
        return count;
    }

    public void setCount(int count) {
        this.count = count;
    }

}
```

可以看到在实体bean中除了正常的教师信息外多了一`count`，它就是mybatis用来判断teacherId是否存在，如果存在就会将存在的个数保存到count中，当然一般Id都是主键，所有count也就一般都是1。下边看一下mybatis的映射文件。

```xml
<insert id="AddTeacher" parameterType="com.mycompany.entity.Teacher">
        <selectKey keyProperty="count" resultType="int" order="BEFORE">
            select count(*) from Teacher where teacher_id = #{teacherId}
        </selectKey>
        <if test="count > 0">
            update event
            <set>
               <if test="teacherName!= null" >  
                    teacher_name= #{teacherName},
               </if>
            </set>
            <where>
                teacher_id = #{teacherId}
            </where>
        </if>
        <if test="count==0">
            insert into teacher(teacher_id,teacher_name) values (#{teacherId},#{teacherName})
        </if>
</insert>
```

可以看到mybatis的实现思路也是先查询Id是否存在，在根据count判断是insert还是update。

## 说明

1.实现原理是`selectKey`做第一次查询，然后根据结果进行判断，所以这里的`order="BEFORE"`是必须的，也是因BEFORE，所以没法通过`<bind>`标签来临时存储中间的值，只能在入参中增加属性来存放。

2.就上面这个例子而言，就要求实体类中包含count属性（可以是别的名字）。否则`selectKey`的结果没法保存，如果入参是个Map类型，就没有这个限制。

3.这种方式只是利用了`selectKey`会多执行一次查询来实现的，但是如果你同时还需要通过`selectKey`获取序列或者自增的id，就会麻烦很多（oracle麻烦，其他支持自增的还是很容易），例如我在上一篇中利用`selectKey` 获取主键Id。

4.建议单独查看学习一下`selectKey`的用法。