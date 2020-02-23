+ **response属性**
  + content  返回的内容
  + charset  编码格式
  + status_code 响应状态码
  + content-type MIME类型 
  + MIME 
    + 互联网邮件传输扩展类型
    + 指定传输的的数据使用哪种形式打开 
    + 大类型/小类型 
      + image/png
      + image/jpg  
  
+ **方法**
  + init  初始化内容
  + write(xxx)  直接写出文本内容
  + flush()  冲刷缓冲区
  + set_cookie(key,value='xxx', max_age=None, exprise=None)
  + delete_cookie(key）删除cookie，上面是设置
  
+ 响应重定向，可实现服务器内部跳转

  + HttpResponseRedict('/grade/2020')   302   条件性转移（临时性转移）
  + views反向解析 url =reverse('namespace:name')
  + 缩写redirect()    301    永久转移
+ reverse（‘namespace：name’）python代码中的反向解析
    + reverse（‘namespace：name' , args=(value1,value2...)）
  + reverse('namespace:name', kwargs={key:value,...})
  
  ## Json
  
  + jsonObject
    + ()
    + key - value
  + JsonArray
    + [  ]
    + 列表中可以是普通数据类型，也可以是jsonObject
  + JsonObject和JsonArray可以嵌套
  + 移动端的json
  + 给Ajax
    + 前后端分离
    + DRF
  + Google CHrome 插件
    + JsonFomatter
    + Jsonview
  
+ JsonResponse
  + 返回Json的请求，通常在异步请求上
    + JsonResponse(dict)
  + content-type是application/Json
  + 重写\__init__ ,序列化Json数据
  
+ HttpResponseBadRequest

  + 400

+ HttpResponseNotFound

  + 404

+ HttpResponseForbidden

  + 403

## 会话技术

- 出现场景
  -  服务器如何识别客户端，让服务器知道你是你
  - Http在Web开发中基本都是短连接
- 请求生命周期
  - 从Request开始
  - 到Response结束
- 种类
  - Cookie
    - 客户端会话技术
      - 数据存储在客户端
    - 键值对存储
    - 支持过期时间
    - 默认Cookie会自动携带，本网站所有Cookie
    - Cookie跨域名，跨网站
    - 通过HttpResponse
    - Cookie默认不支持中文
    - 可以加盐
      - 加密
      - 获取的时候需要解密
  - Session
    - 服务端会话技术
    - 数据存储在服务器中
    - 默认Session存储在内存中
    - Django中默认会把Session持久化到数据库中
    - Django中Session的默认过期时间是14天
    - 主键是字符串
    - 数据是使用了数据安全
      - 使用的base64
      - 在前部添加了一个混淆串
    - Session依赖于Cookie
  - Token
    - 服务端会话技术
    - 自定义的Session
    - 如果用在web页面开发中使用起来和Session基本一致
    - 如果用在移动端或客户端开发中，通常以Json形式传输，需要移动端自己存储Token，需要获取Token关联数据的时候，主动传递Token
  - Cookie和Session，Token的对比
    - cookie使用更简洁，服务器压力更小，但数据不是很安全
    - Session服务器要维护Session 相对安全
    - Token拥有Session的所有优点，自己维护略微麻烦，支持更多的终端
  - CSRF
    - 防跨站攻击
    - 防止恶意注册，确保客户端是我们的客户端
    - 使用了cookie中的csrftoken进行验证，传输
    - 服务器发送给客户端，客户端将cookie获取，还要进行编码转换 ，数据安全
    - 如何实现
      - 在存在csrf_token的标签中的页面中，响应会自动设置一个cookie，
      - 当提交时，会自动验证csrf_token
      - 验证通过，正常执行以后的流程，验证不通过，直接403
    - 算法
      - 编码解码
        - Base64
        - urlencode
      - 摘要算法，指纹算法，杂凑算法
        - MD5  SHA
          - MD5 128位二进制
          - SHA  
        - 单向不可逆的
        - 不管输入多长，输出都是固定长度
        - 只要输入有任意变更，输出都会有巨大变化
      - 加密 
        - 对称加密  
          - 一把钥匙 
          - DES AES
          - 加密解密效率高
        - 非对称加密
          - 两把钥匙
          - 公钥 私钥
          - RSA  PGP 
          - 安全性最高，算法复杂，耗时长

