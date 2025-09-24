# 新增网站

以普通用户身份登录后台，点击左侧菜单“网站管理”-》“我的网站”进去网站列表，点击工具栏上的“新增”按钮，弹出添加网站窗口。如图：
<img width="1008" height="992" alt="image" src="https://github.com/user-attachments/assets/935d5f79-ef61-4c41-b771-5d1bc422dd65" />

## 所属分组 - 可以为空，可以选择一个或多个分组
套餐 - 选择已购买的套餐
域名 - 多个域名已空格分隔
源地址 - 可以为IP，也可以是域名
源端口 - 默认为80

### 批量添加网站
点击左侧菜单“网站管理”-》“我的网站”进去网站列表，点击工具栏上的“新增”按钮，弹出添加网站窗口，在数量栏切换到批量。如图：<img width="998" height="1006" alt="image" src="https://github.com/user-attachments/assets/01c25ac1-e6bd-4dfb-8b79-46e08b4ac6c6" />


```bash
npm install -D vitepress
```

### HTTP设置
<img width="1230" height="278" alt="image" src="https://github.com/user-attachments/assets/06163d1c-c722-48e6-bb8b-93698640fca7" />


HTTPS设置
<img width="1556" height="758" alt="image" src="https://github.com/user-attachments/assets/cb04d6aa-004e-44be-bcac-6d9892d03b0a" />
证书 - 选择使用的证书，可以在左侧菜单手动添加证书，也可以在网站列表，选中此网站一键申请
监听端口 - 默认443，可以监听其它端口，如8443，多个端口以空格分隔
强制HTTPS - 可定义跳转的端口，默认为监听端口的第一个
回源SSL协议 - 回源使用的ssl协议，可选值有SSLv2, SSLv3, TLSv1, TLSv1.1, TLSv1.2, TLSv1.3



### 源站设置

<img width="2446" height="1424" alt="image" src="https://github.com/user-attachments/assets/5d96a9b4-f62a-4fed-b163-ac79c8654872" />

回源协议 - 可选http,https,跟随协议，跟随协议就是访问http的，回源http，访问https，回源https
HTTP回源端口 - 回源协议为http时，回源使用的端口
HTTPS回源端口 - 回源协议为https时，回源使用的端口
负载方式 - ip hash: 同一个IP，始终分配请求到同一台后端服务器，
轮询：按顺序一台台分配请求
url hash：同一个url始终分配到同一台后端服务器
最少连接数：根据Nginx与后端服务器的连接数，选择最少连接的连接
随机：随机分配连接到后端。
源地址 - 可以是IP或域名，不过仅支持一个域名，且不能与IP混合使用。
权重 - 数字越大，权重越大
状态 - 可选上线，下线，备用
健康检查 - 对于设置有多台源服务器的情况，可以用来定时检查设置的后端服务器，自动下线或上线后端服务器
协议：目前只支持http协议的检查，所以回源协议只能是http
域名：检查后端服务器时，使用的域名
路径： 默认为/根目录，可以根据具体情况修改
有效状态码：这里指定后端返回的状态码在此列表的话，认为后端服务器正常，否则认为失败，比如后端返回404的话，就认为后端不正常了。
回源端口映射 - 回源端口跟随访问的端口，如监听了http的81 82端口和监听http2的91 92


安全配置


<img width="3368" height="1732" alt="image" src="https://github.com/user-attachments/assets/348d7492-bc7f-4d2a-a9fb-54f02650f0bc" />

CC防护
默认防护 - 没有开启规则切换且未触发规则切换时的防cc规则，目前内置的规则有宽松，JS验证，5秒盾，点击验证，滑块验证，验证码、旋转图片。
宽松模式适用几乎所有场景，不过对于受到大量cc攻击的时候防御效果差。
JS验证同样需要跳转验证，不过是需要浏览器执行js代码才能得到跳转的URL，不需要人工介入。防御效果很好，推荐网站被攻击时首选使用。
5秒盾访问时会跳出5秒倒计时，5秒后自动验证浏览器
点击验证需要人工点击才能访问防御的网站
滑块验证通过拖动滑动条来验证，防御效果也可以，用户体验影响比验证码损失小
验证码，是一种最严格的防御手段之一，防御效果最强，不过对用户体验影响大
旋转图片，需要用户手动旋转正图片，是一种最严格的防御手段之一，防御效果最强，不过对用户体验影响大
自动提升防护等级 - 可以根据网站的QPS来动态切换或恢复规则。适用于当网站没有被攻击时，使用对用户影响较低的规则，比如宽松模式，然后当QPS突然增大到一定值时，可以认为可能被cc攻击了，然后切换到防御更强的规则，比如滑动验证。这样可以较好的平衡用户体验与网站安全这两方面。
自定义规则 - 当默认规则开启了如浏览器识别，滑动验证，验证码等规则时，如果直接调用API，会触发这些防cc规则，导致访问API失败。这时候可以添加例外，放行这些API。



## 回源配置


<img width="1186" height="400" alt="image" src="https://github.com/user-attachments/assets/7b841034-adde-416f-a082-270a8cf6b235" />

回源域名 - 默认为访问的域名，即客户通过www.cdnfly.cn访问网站，回源也使用www.cdnfly.cn，也可以自定义成其它的域名
Range回源 - cdnfly在缓存资源时，为提高存储效率会将文件进行切片存储，并且支持 Range 请求，若请求时携带 HTTP 头部Range: bytes = 0-999，则返回文件的前1000个字节给用户。
开启 Range 回源配置，若用户请求的部分文件已过期，CDN 会根据用户请求进行分片回源，仅拉取用户需要的部分文件进行缓存，同时返回给用户；关闭 Range 回源配置，即便用户请求的是部分文件，CDN 在回源时仍会拉取整个文件，而后进行缓存，并响应给用户其要求的部分文件。
开启 Range 回源配置能够有效提高大文件分发效率，提升响应速度，降低源站压力。


### 高级配置


压缩设置
可开启或关闭gzip压缩，并定义需要压缩的文件类型

Websocket配置
开启后，nginx就可以代理websocket的请求了

错误页面配置
支持自定义404和50x页面

源站请求头
即在回源时，附加一个请求头回源。系统默认传X-Real-IP请求头，值为客户端的IP给源服务器。也可以设置其它的请求头，附加客户IP，如

<img width="1050" height="636" alt="image" src="https://github.com/user-attachments/assets/0a601228-9735-4df7-a9a0-4a43cd845045" />

URL转向
此URL转向功能使用的是Nginx的rewrite模块，更详情的说明参考http://nginx.org/en/docs/http/ngx_http_rewrite_module.html#rewrite

<img width="1004" height="836" alt="image" src="https://github.com/user-attachments/assets/384e13f3-7244-4baa-bc69-77efc2e42f77" />



### 缓存配置

缓存配置，是使用Nginx proxy模块，更多的说明请参考http://nginx.org/en/docs/http/ngx_http_proxy_module.html

<img width="1586" height="1092" alt="image" src="https://github.com/user-attachments/assets/ad64c690-1f48-46f6-96d7-ab1ea5656510" />

类型 - 可选后缀名，目录，全路径
选择后缀名时，内容填写如css|js|png，不区分大小，表示缓存后缀为css,js,png的请求，如http://www.cdnfly.cn/123.css
选择目录时，内容填写aa|bb|cc，表示缓存如http://cdn.cn/aa/11.php,http://cdn.cn/aa/22.jsp的请求
选择全路径时，内容填写/123.css，表示只缓存http://cdn.cn/123.css的请求
有效期 - 输入数字，单位可选秒，时，天
忽略参数 - 启用时，忽略url的参数，如/123.css与/123.css?a=1，这两个请求只缓存一份，请求时/123.css,/123.css?a=2,/123.css?b=3都是认为已经缓存了，取与/123.css同样的缓存
强制缓存 - 当想要缓存动态内容时，或者发现设置了缓存但实际没有生效，可以开启这个
不缓存条件 - 设置某一特定的请求不缓存，比如缓存了整个网站除了客户端带指定cookie名为wordpress_logged_in的请求，那么可以变量输入$http_cookie，字符串输入wordpress_logged_in。

刷新预热

刷新缓存

可刷新具体的URL，也可刷新整个目录下的文件

预热URL

为了提高缓存命中率和首个用户的访问速度，可以在用户访问之前，先预热下资源

### 证书管理
可独立的管理所有证书，可自己续期Let's encrypt的证书，查看所有证书的过期时间等

上传自己的证书
如图，可以上传自己已经申请好的证书，之后绑定到网站上使用

<img width="1424" height="1256" alt="image" src="https://github.com/user-attachments/assets/6b1734bb-ed77-41f7-9e22-e83bbbf4b8c2" />

申请Let's encrypt证书

如图可申请 www.cdn.cn cdn.cn的Let's encrypt免费证书，如果不指定DNS API，www.cdn.cn和cdn.cn需要预先解析到cdn的节点。如果指定了DNS API就不需要，DNS API是cdn.cn域名所在DNS提供商的API密钥。

<img width="1410" height="1220" alt="image" src="https://github.com/user-attachments/assets/3293fba0-144f-44d6-b96d-9a4848e23381" />
Let's encrypt支持申请通配符证书，不过只支持dns的验证方式，所以必须指定申请域名的DNS API，如图

<img width="1418" height="1052" alt="image" src="https://github.com/user-attachments/assets/e2211576-e228-4ac7-861e-239653904269" />

支持批量申请Let's encrypt证书，只需要一行输入一个或多个域名就行，如图

<img width="1408" height="876" alt="image" src="https://github.com/user-attachments/assets/a86fb469-7b46-4ca0-9ffb-ce2167e7f8d1" />

当然，系统还提供了一键申请Let's encryp一个或多个网站的功能，进一步方面域名证书的申请，如图：

<img width="928" height="406" alt="image" src="https://github.com/user-attachments/assets/f9ac1b6f-b488-43e5-9eb4-c5c7abfae091" />




## CC规则

防cc规则主要由三部分组成匹配器，过滤器，动作。

匹配器: 用来匹配用户的请求，可以匹配用户IP,Host,req_uri(带参数),uri(不带参数),user_agent和referer。一个匹配器可以有多个匹配项，添加多个匹配项时，此匹配器所有的匹配项都满足时，这个匹配器才为真。如果匹配了请求，就使用下面的过滤器来对请求进行验证。
过滤器: 用来对客户请求进行验证，比如统计请求数是否超限，是否输入对验证码，是否跳转到正确的URL等，如果验证次数超过指定次数，那么就执行下面指定的动作来拦截。
动作: 当请求无法通过过滤器时，执行相应的动作。

匹配器
匹配器由匹配项，操作符，匹配值组成。比如匹配项是IP，操作符是=，匹配值是192.168.0.1，表示客户端IP是192.168.0.1才算匹配。

<img width="866" height="892" alt="image" src="https://github.com/user-attachments/assets/6b9edeb3-7d4a-4046-9453-02d135f64b93" />

IP地址 - 客户端IP地址
域名 - 客户请求的域名
请求URI - 请求的url，如/123.php?a=1，保留参数匹配。
请求URI(不带参数) - 去除参数的url，如原始/123.php?a=1，经处理变成/123.php再去匹配
请求方法 - 如GET, POST等
浏览器UA - 浏览器名称，如Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.116 Safari/537.36
国家代码 - 由于两位字母表示某个国家的IP地址，比如CN表示在中国网络下请求网站的客户，完整的国家代码列表https://www.iban.com/country-codes

<img width="946" height="882" alt="image" src="https://github.com/user-attachments/assets/6443b781-e4bf-427a-8a40-db0f3862a90a" />

等于 - 即与匹配值完全匹配条件才成立
不等于 - 参考等于
包含- 要匹配的值包含有匹配值条件就成立，如请求URI为/index.php，匹配值为php的话，条件成立
不包含 - 参考包含
前缀匹配 - 即从前面开始匹配，如请求URI为/api/index，当匹配值为/api时，条件成立，值为index时，条件不成立
后缀匹配 - 即从尾部开始匹配，如请求URI为/api/index，当匹配值为index时，条件成立，匹配值为/api时，条件不成立
正则匹配 - 如^/[0-9]+，即匹配以/开头，后面接数字的URI

过滤器

<img width="1162" height="1112" alt="image" src="https://github.com/user-attachments/assets/180ac9c3-25e3-41f7-984b-28675faf54be" />


请求速率

限制客户在一定时间内的总请求次数。可以限制总的URL请求数，也可以限制同一个URL累积的请求数。

302跳转
当客户请求cdnfly节点时，cdnfly会302返回一个url，客户跟随访问这个URL才算验证通过，否则算失败。

浏览器识别
客户请求cdnfly节点时，cdnfly返回一段带跳转功能的js代码，客户跟随访问这个URL才算验证通过，否则算失败。

滑动验证
客户请求cdnfly节点时，cdnfly返回一个滑动条，客户需要拖动滑动条才算验证通过，否则算失败。

验证码
客户请求cdnfly节点时，cdnfly返回一个验证码，客户需要输入正确的验证码提交才算验证通过，否则算失败。

URL鉴权

url鉴权过滤器适用时API类防cc攻击。需要与客户端配合，cdn定义一个密钥，客户端md5如uri,时间戳,随机数,密钥，得出的值传给cdn验证，验证失败到一定次数将拉黑这个IP。URL鉴权提供两种鉴权方式，A和B。

方式A

URL格式为http://DomainName/img/FileName?sign=md5hash&t=timestamp
timestamp为当前时间戳，如1598342331（签名用的时间戳与参数t的时间戳需要一致），md5hash为md5(密钥uri时间戳)，如果开启IP鉴权（客户端IP地址为192.168.0.8），那么md5hash为md5(密钥uri时间戳IP地址)， 其中密钥为在cdn定义好的密钥，md5hash为32位，uri为不带参数的路径，且要转为小写再做md5，如/img/filename，时间戳为1598342331(精确到秒就行)
方式A的设置如下


<img width="894" height="964" alt="image" src="https://github.com/user-attachments/assets/5db539ac-aa8c-4402-947c-8c4c45bc47a3" />


n秒内，最大失败次数 - 即如果在60秒内，验证失败超过5次的话，拉黑IP

鉴权方式 - 这里选TypeA

密钥 - 与其它数据一起md5得到的hash，客户端同样使用这里定义的密钥来md5
签名参数名 - 默认为sign

时间戳参数名 - 默认t

最大时间相差(秒) - 允许上下相关多少秒，超过此范围签名认为无效

签名使用次数 - 带同一个签名的url允许访问的次数，0为不限制，越过限制则拉黑IP


javascript示例代码：


// 获取时间戳
let timeStamp = Date.parse(new Date()) / 1000;

// 将要请求的原始url
let url = "http://for-test.cdnfly.cn/index.php?model=abc"

// 从原始url中获取其路径
let urlObj = new URL(url)
let path = urlObj.pathname.toLowerCase()

// cdn后台配置的密钥
let key = "KRcz58Wn4yBprtc2"

// 对密钥、路径、时间戳md5签名
let sign = md5(key+path+timeStamp)

// 生成新的请求url
if (urlObj.search == "") {
	let newUrl = url+"?sign=" + sign+"&t="+timeStamp
} else {
	let newUrl = url+"&sign=" + sign+"&t="+timeStamp
}
console.log(newUrl)


### Build for Production


### Deploy to GitHub Pages



### Netlify Deployment

## Best Practices

### File Organization


### Navigation Structure

### Content Guidelines
