# Python 实现腾讯云动态域名解析

操你妈的腾讯云, 垃圾API还有一堆乱七八糟的鉴权, 哪有那么多逼逼赖赖的麻烦



### 生成一个初始请求字符串

1. 确定请求类型, 请求的目标, 供计算签名使用

2. 计算签名

   计算签名使用的是HMAC-SHA256算法, 使用python自带的`hmac`, `hashlib` ,完成计算之后再用`base64`编码成16进制. 网上很多文章都是抄来抄去, 全是2.7版本的. 我亲自去研究了一下python3.6的文档. 两个文档的链接可以从这里找到: [hashlib](https://docs.python.org/3.6/library/hashlib.html), [hmac](https://docs.python.org/3.6/library/hmac.html), 最后用[base64](https://docs.python.org/3.6/library/base64.html)来进行编码. 

   ```python
   def caculateSignature(SecretKey, requestString):
       secret = SecretKey.encode('utf-8')  #  秘钥
       data = requestString.encode('utf-8')  #  加密数据
       signature = base64.b64encode(hmac.new(secret, data, digestmod=hashlib.sha256).digest())
       return signature
   ```

   注意, 返回的字符串需要通过web库编码成http字符串的形式。 这个之后会讲。

1. 查询地区, 获得地区代码

   这里涉及到一个问题, 解析返回的json, 使用的是Python的json包, 文档在[这里](https://docs.python.org/3.6/library/json.html).

   之后就是按照腾讯云的官方文档把数据获取下来就可以了。有了地区代码之后， 整个请求字符串就能拼出来了。因为这个东西依赖于腾讯云的api，我说多少都没用，腾讯云的api一换我说的都白瞎了。最好的办法还是自己去查最新的文档比较好。
   
   至于拼接字符串，其实我用的办法很笨就是把那几个字符串变量用加号`+`拼起来。没什么难度。
   
   

### 动态域名解析的逻辑



