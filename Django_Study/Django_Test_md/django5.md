- **迁移**
  
  - 分两步 1.生成迁移 2.执行迁移
  - 迁移文件的生成
    - 根据models生成对应的对应文件
    - 根据models和已有迁移文件差别，生成新的迁移文件
  - 执行迁移文件
    - 先在迁移记录查找，哪些文件未迁移过
      - app_label + 迁移文件的名字
    - 执行未迁移的文件
    - 执行完毕，数据库记录执行的迁移文件
  - 重新迁移
    - 删除迁移文件
    - 删除迁移文件产生的表
    - 删除迁移记录
  - **模型关系**
    
    - 1：1
      
      - 应用场景
        - 用于复杂表的拆分
        - 扩展新功能
        
      - Django中OneToOneField
        - 使用时关系声明还是有细微差别 
        - 外键值在整个表中值只允许有一个
        
      - 删除数据
      
        - 级联表
      
          - 主表  
      
          - 从表  主表数据删除，从表自动删除
      
          - 谁声明关系谁就是从表
      
	        - 开发中如何确认主从
  	  
    	      - 当系统遭遇不可避免的毁灭时，只能保留一张表，这个表就是你的主表
      - 默认特性（CASECADE）
        
        -  从表数据删除，主表不受影响
        
          - 主表删除数据，从表数据删除
          - PORTECT受保护
              - on_delete=models.PORTECT
              - 开发中防止误删，会执行此操作
              - 主表如果存在级联数据，删除动作受保护，不能成功
              - 主表如果不存在级联数据，可以删除成功
        - SET
          - SET_NULL
          - SET_DEFAULT
          - SET()
        - 级联数据获取
          - 主获取从 隐形属性 默认就是级联模型的名字
          - 从获取主  显性属性 ，就是属性的名字
      
    - 1：n
    
      - ForeignKey
      - 主从获取
        - 主获取从  隐形属性  级联模型_set
          - student_set  Manager的子类
            - all
            - filter
            - exclude
        - 从获取主 
          - 显性属性
    
    - m：n
    
      - 产生单独的关系表
        - 关系表中存储级联表的主键，通过多个外键实现的
        - 多个外键值不能同时相等
        
      - 级联数据
        - add
        - remove
        - get
        
      - ManyRelateManager
        - 函数中定义的类
        - 父类是一个参数--动态创建
        
      - 级联数据获取
        - 从获取主
          - 删或者添加一个重复的数据，不会重复操作，也不会报错
        - 主获取从
        
      - ```python
        customer = Customer.objects.last()
        goods = Goods.objects.last()
        goods.g_customer.add(customer)  # 从获取主
        goods.g_customer.remove(customer)customer.goods_set.add(goods)   # 主获取从
        ```
      
    - **模型继承**
    
      - Django中模型支持继承
    
      - 默认继承将通用字段放到父表中，特定字段放到自己的表中，中间使用外键连接
    
        - 关系型数据库关系越复杂，效率越低，查询越慢
        - 父类表中也会存储过多的数据
    
      - 使用元信息来解决这个问题
    
        - 使模型抽象化，抽象的模型不会在数据库中产生映射了
    
        - 子模型映射处来的表直接包含父模型的字段
    
        - ```python
          class Animal(models.Model):  #不会在数据库中建表  
          	a_name = models.CharField(max_length=16)       	 	class Meta:       
                  	abstract = Trueclass Cat(Animal):  
                          
          class Cat(Animal): #数据库所建的表有Animal的属性
          	a_eatmodels.CharField(max_length=32)
        ```
    
  - **企业开发中**
  
    - model->sql
      - Django 支持
    - sql->model
      - 创好表，在要导入的工程组好配置
      - 执行命令        python manage.py inspectdb > App/models.py
      - 元信息中包含一个属性 manage = False，
      - 自己的某个模型不想被系统迁移管理 也可以使用 manage = False
  
  - **静态static文件配置**
  
    - 这个静态文件主要用来放置CSS   HTML    图片    字体文件等
    - STATICFILES_DIRS = [   os.path.join(BASE_DIR, 'static'),  ]
    - 模板中的声明
      - {%load  static%}
    - 在引用资源的时候用
      - {% static  ‘xxx’  %}   xxx就是相对于staticfiles_dirs的一个位置
  
  - 指定传输文件夹位置  
  
    - MEDIA_ROOT = os.path.join(BASE_DIR, 'static/upload')
  
    - ```python
      class UserModel(models.Model):    
          u_name = models.CharField(max_length=16)    
          # upload_to是相对路径， 相对于MEDIA_ROOT    媒体根目录    
          u_icon = models.ImageField(upload_to='icons')  # upload_to='%Y/%M/%D/icon'可以在文件夹以年月日分级
      ```