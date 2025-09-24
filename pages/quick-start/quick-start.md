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

```bash
mkdir docs
echo '# Hello VitePress' > docs/index.md
```

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



```js
// .vitepress/config.js
import { defineConfig } from 'vitepress'

export default defineConfig({
  title: 'My Docs',
  description: 'My documentation site'
})
```

## 回源配置


<img width="1186" height="400" alt="image" src="https://github.com/user-attachments/assets/7b841034-adde-416f-a082-270a8cf6b235" />

回源域名 - 默认为访问的域名，即客户通过www.cdnfly.cn访问网站，回源也使用www.cdnfly.cn，也可以自定义成其它的域名
Range回源 - cdnfly在缓存资源时，为提高存储效率会将文件进行切片存储，并且支持 Range 请求，若请求时携带 HTTP 头部Range: bytes = 0-999，则返回文件的前1000个字节给用户。
开启 Range 回源配置，若用户请求的部分文件已过期，CDN 会根据用户请求进行分片回源，仅拉取用户需要的部分文件进行缓存，同时返回给用户；关闭 Range 回源配置，即便用户请求的是部分文件，CDN 在回源时仍会拉取整个文件，而后进行缓存，并响应给用户其要求的部分文件。
开启 Range 回源配置能够有效提高大文件分发效率，提升响应速度，降低源站压力。


### Custom Theme

You can customize the theme by creating your own theme files:

```js
// .vitepress/theme/index.js
import DefaultTheme from 'vitepress/theme'
import './custom.css'

export default DefaultTheme
```

### Markdown Extensions

VitePress supports various markdown extensions:

::: tip
This is a tip box
:::

::: warning
This is a warning box
:::

::: danger
This is a danger box
:::

### Code Highlighting

VitePress provides excellent syntax highlighting:

```js
function hello() {
  console.log('Hello, VitePress!')
}
```

```css
.custom-style {
  color: #42b883;
  font-weight: bold;
}
```

## Deployment

### Build for Production

```bash
npm run docs:build
```

### Deploy to GitHub Pages

1. Push your code to GitHub
2. Enable GitHub Pages in repository settings
3. Set source to GitHub Actions
4. Create deployment workflow

### Netlify Deployment

1. Connect your repository to Netlify
2. Set build command: `npm run docs:build`
3. Set publish directory: `docs/.vitepress/dist`

## Best Practices

### File Organization

Organize your documentation with a clear structure:

```
docs/
├── guide/
│   ├── getting-started.md
│   ├── installation.md
│   └── configuration.md
├── reference/
│   ├── config.md
│   └── theme.md
└── index.md
```

### Navigation Structure

Use clear and logical navigation:

- Group related pages together
- Use descriptive titles
- Keep navigation depth reasonable (2-3 levels max)

### Content Guidelines

- Write clear, concise content
- Use code examples where helpful
- Include screenshots for complex features
- Keep pages focused on a single topic 
