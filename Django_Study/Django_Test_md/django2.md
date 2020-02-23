+ **定义模型**
	+ 模型->表、属性->字段->一列
	+ 数据库数据类型
	+ 字符串，数字，日期时间
+ **mdoel函数**
	+ objects  all()   拿所有
	+ get()  指定拿某一个
	+ order by() 排序
	+ values（） 将数据库中的每一行键和键值放到字典，再存放到列表
	+ first()获取第一个
	+ last()获取最后一个 可能会出现first()和last()是同一个，解决：手动写排序规则
	+ count()  返回查询的个数
+ **模型过滤**
	+ filter()  返回符合筛选条件的数据
	+ exclude()  返回不符合筛选条件的数据集
	+ 可以连续使用 Person.objects.filter().exclude().XXX
	+ filter，exclude all 都不会真真的去查询数据库，在迭代结果集或获取单个对象属性的时候，它才会去查询数据库  懒查询：为了优化结构和查询

+ **快捷键** 
	+ .re 快捷生成return


__init__在父类models.Model中已被占用，在自定义的模型中无法使用
对象方法：可以调用对象的属性也能调用类的属性
方法：不能调用对象属性，只能调用类属性
静态方法：不能调用对象属性，也不能调用类属性，只是寄生在这个类上而已

+ **客户端错误代码**
	+ 2XX:请求成功
	+ 3XX:请求重定向，请求转发
	+ 4XX:客户端错误
	+ 5XX:服务器错误后端开发人员最不想看到的


+ **切片(不同于python)**
	+ QuerySet[5:15] 获取5-14条数据（左闭右开），下标不能是负数
	+ 相当于sql中的limit和offset


+ **查询条件**
	+ 属性__运算符 = 值
	+ gt    大于
	+ It    小于
	+ gte   大于等于
	+ Ite    小于等于
	+ in在某一个集合之中 
	+ contains 包含 模糊查询like
	+ starts with     endwith      以XXX开始结束本质是like
	+ **前面同时添加i，ignore忽略大小写**
        + iexact 
        + icontains
        + istartwith
        + iendwith
+django时区  
	+ 1.关闭django自定义时区setting->USE_TZ=False   2.在数据库中创建对应的时区


grades = Grade.objects.filter(students__s_name='jack')#查询哪些班级有Jack


+ **聚合函数**
	+ aggregate()
	
	+ Avg: 平均值 Count: 数量 Max: 最大 Min:最小  Sum: 求和
	
	+ Students. objects.aggregate(Max('age'))#查询age属性的平均值
	
+ **F对象**
	
	+ 可以使用模型A的属性与B属性比较
	+ grade = Grade.objects.filter(g_girl_numgt=F('g_boy_num'))#查询g_girl_num大于g_boy_num的班级
	+ F对象支持算数运算
	+ grades = Grade .objects.filter(g_girl_numgt=F('g_boy_num')+10)

+ **Q对象**
	+ 过滤器方法中的关键参数常用于组合条件
	+ 年龄小于25且女生人数大于30
		+ Students.objects.filter(Q(s_agelt=25) & Q(s_girl_numst=30))
	+ Q对象语法支持 | or & and  ~（取反）
	+ 年龄大于等于的
		+ Students.objects.filter(~Q(s_age__lt=25 ))

+ **模型成员**
	+ 显性属性：开发者手动书写的属性
	+ 隐形属性：开发者没有书写ORM自动生成的，如果手动声明，系统不会自动产生隐形属性
	+ objects modelmanager的一个成员
```python
  class Animal(models.Model):
                a_m = models.Manager()	#objects就不存在了             
```

