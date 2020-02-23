+ **连接数据库需在库名后添加：**?serverTimezone=GMT
+ **库表外键需添加参数 ：**on_delete=models.CASCADE

+ **国内源**  
  + https://pypi.douban.com/simple
+ **建工程命令**  
  +  django-admin startproject xxx
+  **项目结构**  
  +  xxx-manage.py（管理整个项目的文件，命令通过它调用）
	    -settings （项目全局配置文件）
	    -urls（根路由）
	    -wsgl（用在以后项目部署上，前期不用）
+启动项目   
	+ python manage.py runserver [ip] [端口]（0.0.0.0代表所有ip）
+ **创建一个Application**
	+ python manage.py startapp APP
+ **Application结构**
	+ -views
		-modles
		-admin（后台管理）
		-apps（应用配置）
		-tests（单元测试）
		-migrations-迁移目录
	    -将App注册到setting中installed_Apps中
+ **编写要求**
	+ Briwser->urls->views->models->views->response
+ **添加urls**
	+ url(r''(正则匹配规则), views.XXX(对应的视图函数))
+ **编写视图函数**
	+  默认传入的参数为requests，必须返回一个response（HttpResponse，render（渲染，简写））
+ **sqllite(轻量级数据库)**
	+ 修改数据库
		+ settings->DATABASE中修改参(NAME,ENGINE,USER,PASSWORD,HOST,PORT)
	+ 迁移
    	+生成迁移-->python manage.py makemigrations
      	执行迁移--生成新的数据库产生表-->python manage.py migrate
+数据操作
	+ 增--创建对象进行save()   
    + 查--模型.objects.all()--模型.objects.get() 
    + 更新--基于查询--修改属性值--save() 
    + 删除--基于查询--delete()
+ **显示在模板中**
	+ 先挖坑{{var}}--再填坑--渲染模板的时候传递上下文(字典)进来--key,value
+ **shell终端**
	+ python manage.py shell-->django中端-->集成了django环境的python终端-->通常用来调试
+ **html技巧**
	+ ul>li
      ul****5***
      ul>li*5
      ul->tab->for->tab
      shift+F6   重命名，重构式的
+ **快捷键**
	+ 查看所需参数ctrl+p
