# spider
微博，163邮箱，贴吧，天涯论坛
Python模拟登陆（微博）
1、预登陆，在用户输入用户名之后会进行预处理和加密，抓包可以看到服务器返回的一系列字段，提取字段，提取哪些字段在第二部可以看到。
2、登陆，登陆过程抓包，可以发现一条post请求：
https://login.sina.com.cn/sso/login.php?client=ssologin.js(v1.4.19)
多次抓包可以发现其中变量，servertime、nonce字段，用于密码加密的RSA公钥不变，分别是10001和1330428213，从js文件中可以发现用户名是通过base64编码的，密码是通过RSA2加密的。
3、输入用户名和密码，传入用户名和密码加密函数
4、Cookie和urllib2结合进行模拟登陆，捕获cookie在后续的使用中重新调用
            #获取一个保存cookies的对象
            cj = cookielib.CookieJar()
            #将一个保存cookies对象和一个HTTP的cookie的处理器绑定
            cookie_support = urllib2.HTTPCookieProcessor(cj)
            #创建一个opener,设置一个handler用于处理http的url打开
            opener = urllib2.build_opener(cookie_support, urllib2.HTTPHandler)
            #安装opener，此后调用urlopen()时会使用安装过的opener对象
            urllib2.install_opener(opener)
5、构造post表单。
6、Urllib2.request（URL，data，headers）
Urllib2.urlopen（）
7、正则表达式获取重定位网址并打开
8、访问主页
