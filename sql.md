
当我在将大小写忽略的时候之前使用大写的数据库的名字就进不去了,因为系统自动将我打的大写换成了小写.....

每一个检查点都会记录他自己的操作对象的信息状态,当共用的是同一个硬盘上的数据,硬盘上的数据是会被最近的检查点所覆盖掉的,当要回复在之前的某一个特定的检查点的时候,是先通过最近的检查点来逐级向上恢复的

#### 当colume 与condition 条件相等时结果为result
```
case colume
    when condition then result
    when condition then result
    when condition then result
else result
end
```

#### 当满足某一条件时，执行某一result
```
case  
    when condition then result
    when condition then result
    when condition then result
else result
end
```
#### 当满足某一条件时，执行某一result,把该结果赋值到new_column_name 字段中
```
case  
    when condition then result
    when condition then result
    when condition then result
else result
end new_column_name
```
case when 用在select 语句中，新的字段new_column_name可以用来排序，但是不能用在where中
