---
title: javaweb-DBUtils
---
常规方式获取数据库中的数据：

```java
while(resultSet.next()){
	Integer id=resultSet.getInt(1);
	String name=resultSet.getString(2);
	Double score=resultSet.getDouble(3);
	Date birthday=resultSet.getDate(4);
	student=new Student(id,name,score,birthday);
}
```

数据库一条记录中有N项就要获取N次，再赋值给java对象，很繁琐。
`DBUtils`可以帮助开发者完成数据的封装（结果集到java对象的映射）。
具体使用：
注:需要先导入jar包
`QueryRunner`是`DBUtils`中的类。
`query(Connection,String,ResultSetHandler<T>,Object... params)`其中`ResultHandler<T>`是用来处理结果集的，可以将查询到的结果集转换成对应的java对象，提供了4种实现类:

- `BeanHandler`：将结果集映射成Java对象`Student`
- `BeanListHandler`：将结果集映射成List集合`List<student>`
- `MapHandler`：将结果集映射成`Map`对象
- `MapListHandler`：将结果集映射成`MapList`集合

而`params`是赋值给`sql`语句中变量的参数，下面这段代码中传递的是变量id。

```java
try{
	Connection connection=dataSource.getConnection();
	String sql="select * from student where id = ?";
	QueryRunner queryRunner=new QueryRunner();
	Student student=queryRunner.query(connection,sql,new BeanHandler<Student>(Student.class),id);
}
```



