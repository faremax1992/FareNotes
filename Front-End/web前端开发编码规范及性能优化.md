<!-- MarkdownTOC -->

- [代码优化](#%E4%BB%A3%E7%A0%81%E4%BC%98%E5%8C%96)
  - [HTML+CSS](#htmlcss)
  - [JavaScript](#javascript)
- [性能优化](#%E6%80%A7%E8%83%BD%E4%BC%98%E5%8C%96)
  - [页面渲染](#%E9%A1%B5%E9%9D%A2%E6%B8%B2%E6%9F%93)
    - [减少页面 reflow](#%E5%87%8F%E5%B0%91%E9%A1%B5%E9%9D%A2-reflow)
    - [优化用户体验](#%E4%BC%98%E5%8C%96%E7%94%A8%E6%88%B7%E4%BD%93%E9%AA%8C)
    - [代码优化](#%E4%BB%A3%E7%A0%81%E4%BC%98%E5%8C%96-1)
  - [网络通信](#%E7%BD%91%E7%BB%9C%E9%80%9A%E4%BF%A1)
    - [减少通信链接次数](#%E5%87%8F%E5%B0%91%E9%80%9A%E4%BF%A1%E9%93%BE%E6%8E%A5%E6%AC%A1%E6%95%B0)
    - [减少数据传输距离和数据大小](#%E5%87%8F%E5%B0%91%E6%95%B0%E6%8D%AE%E4%BC%A0%E8%BE%93%E8%B7%9D%E7%A6%BB%E5%92%8C%E6%95%B0%E6%8D%AE%E5%A4%A7%E5%B0%8F)
    - [合理利用服务器资源](#%E5%90%88%E7%90%86%E5%88%A9%E7%94%A8%E6%9C%8D%E5%8A%A1%E5%99%A8%E8%B5%84%E6%BA%90)
  - [SEO](#seo)
  - [综合优化](#%E7%BB%BC%E5%90%88%E4%BC%98%E5%8C%96)

<!-- /MarkdownTOC -->

# 代码优化
> 这个部分仅仅将代码优化本身,不考虑性能,关于代码部分的性能优化在 **页面渲染** 部分 **代码优化** 中

## HTML+CSS
- 符合 XHTML 规范: 小写,正确嵌套,必须关闭;
- 双引号,合理缩进,utf-8编码;
- 标签语义化,便于维护;
- 合理注释,比如 div 关闭的地方表明配对的 div;
- HTML,CSS,JS 分离,方便维护;
- 避免使用 iframe, 否则会阻塞父文档 onload;
- 样式继承,不要重复;
- 不要乱用 href 和 onclick, 他们本质不同,href 偏向资源加载,而 onclick 仅仅是点击;其次 click 事件在 href 之前执行;
- css伪类选择器不宜太多,防止选择器过载;
- 不要让样式难以覆盖,少用`!improtant`;
- 善于利用样式继承(注意继承和层叠是不一样的概念);
- 不要保留过时的浏览器前缀和兼容性写法;

## JavaScript
- 标识符简短清晰,不用 1 和 0 代替 true 和 false,合理编写注释,提高代码可读性;
- 定义变量一定写 var,以免污染全局,同时,new Function() 和 eval() 也会污染全局;
- 长字符串用字符串链接写法,而非跨行。在兼容的情况下,用 ES6 中的多行字符串也更好;
- 不要在 if 和 for 中定义函数,前置没有意义,破坏分支;后者易出现循环参数拖尾的情况;
- 在此法作用域开始处声明变量,提高可读性;
- `var Name = function Name(){}; ` 有利于堆栈跟踪(注意变量名一致性);
- 位运算不要大于32位;
- 不要随意重写已有原型,可以用其实例化对象代替,实现实例继承;
- 对象方法尽量返回 this 以便链式调用;
- 函数的放入同名文件夹中,定义 noConflict 方法导出前一版本并返回当然版本;
- 设计封装(类,闭包,模块)时,尽量使用严格模式;
- 在内容为 js 的 script 标签上和内容为 css 的 link 标签上省略 type 属性和 lang 属性;
- 注意变量名不要使用保留字和系统全局变量(方法)一样;
- 以下行为污染全局: setTimeout 和 setInterval 的首参传入字符串; eval()函数; new Function() 构造函数。

#性能优化

## 页面渲染

### 减少页面 reflow
- 修改元素多个样式可以通过修改 className 完成,这样可以把多次 reflow 减少为一次 reflow;
- 修改元素多个样式可以分为三步：先隐藏(display:none), 再修改,最后显示。这样可以把多次 reflow 减少为两次次 reflow;
- 添加页面内容可以通过将所有内容写入 docuemnt fragment 元素后再一次性 append 到页面中;
- 添加页面内容可以通过将所有内容组成长字符串,再一次性编辑 innerHTML 加入到页面中;
- css(style 标签和 link 标签) 放在 head 中,这样浏览器在加载数据时候可以直接通过 css tree 生成 render tree, 减少不必要的重新渲染;
- 在不影响视觉效果的情况下,尽量减少 js 动画精度;
- div 布局优于 table 布局,因为后者中元素任意属性改名都会对整个表进行回流;

### 优化用户体验
- 使用懒加载技术,保证首屏优先加载;
- 使用异步脚步,不阻塞主页面渲染;
- 先渲染界面,在不影响首屏情况下,使用 js 脚本动态加载后续数据;
- 将不影响渲染的脚本后置(放在 body 之后),优先渲染;
- 添加自定义的错误页面（如404 not found 页面）;
- 利用 GPU 加速;

### 代码优化
- 图片 img 标签的 src 不要空着,以免产生多余请求;
- href, url()和 src 中的链接,用`//`代替`http://`,`/content/a.jpg`代替`content/a.jpg`, 被替代的后者会多发送一个 http 请求;
- 合理优化外链 css 和 JS 以利用缓存;
- 资源控制在25kB之内,否则移动端可能无法缓存;
- 减少不必要的 DOM 节点;
- 十六进制颜色优于 rgb/hsl 函数,图形转换优于动画,css 动画优于 js 动画,少用 hack 写法;
- 尽量避免 css 表达式;
- 不要重复加载相同代码;
- 利用事件委托减少事件定义;
- 利用变量保存多次用到的 DOM 查询结果,减少反复查找;
- 能用 !== 或 ===,就不要用 != 或 ==,减少不必要的隐式类型转换;
- 尽量使用现有的函数方法,比如数组所有元素求和,直接用 reduce 方法, 再考虑用 map 方法,接着考虑 forEach 方法,然后是 for...in, 最后是 for;
- 利用 {} 或 [] 定义对象或数组,比 new Object() 或 new Array() 效率高;
- 避免 String 类型隐式装箱（隐式调用 new String());
- 用 switch 代替过多的 if, 并按判断条件的可能性排序,以便尽早结束判断;
- [].join() 动态生成字符串比字符串链接(+)性能更好;
- nextSibling() 性能比 children 好；
- cloneNode() 比 createElement() 效率高；
- 考虑在页面渲染完毕以后再动态加载辅助用的外部 js 脚本；

## 网络通信

### 减少通信链接次数

- css spirit 将多次请求变为1次请求;
- 设置 http头的属性：connection: keep-alive,使得链接为长连接,减少频繁的握手挥手过程;
- 设置合适的 http头的属性：expires, cache-control 和 max-age
- 合理利用浏览器本地缓存,路由缓存,使得一些数据不需要从服务器获取;
- 去除不必要的重定向;
- 合并文件 如 css js脚本;
- 保存(缓存)必要的 Ajax 请求数据;

### 减少数据传输距离和数据大小
- 压缩代码;
- 使用内容分发网络(cdn), 如 Akamai, Limelight等;
- 使用 Gzip 压缩;
- 使用新的图片格式或矢量图,如 `.apng`, `.webp` 和 `.svg`;
- 必要时, 减小 cookie, 以减少 http 请求中的数据量;
- 尽量用缩写的 css 样式;
- 合理利用服务器缓存,cdn缓存;
- 尽量少用或不用 ETag,一般情况下 Expires 头已经够用了;

### 合理利用服务器资源
- 使用负载均衡技术,如硬件技术：Alteon, F5和软件技术：Nginx, LVS;
- 减少 DNS 查找时间(控制在20ms~100ms);
- 设置图片服务器;
- 增加 TTL 时长,建议为24hours(引自Steve Souders的《High Performance Web Sites》)

## SEO
- 完善 meta 标签,discription 简洁明了,keywords 清晰;
- 重要内容不要用 js 或后端语言加载;
- 合理利用 h标签,尤其 h1 标签,有很高权重;
- 图片写上合理的 alt 值;
- URI 控制在 256KB 之内;
- 不要使用 iframe;
- 语义化标签的使用;

## 综合优化
- 用多个域名存储网站资源(减小cookie, 节约主域名连接数,突破浏览器并发限制,优化cdn缓存)
- 使用 base64 Encode 图片,减小链接数量和传输大小。
