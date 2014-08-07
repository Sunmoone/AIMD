IE8兼容性视图解决方案【技术文档】
==========

##问题描述

1. 使用IE8+正常访问网页时，会自动切换至兼容性视图
2. 使用IE8+正常访问网页时，不定时的会从标准视图切换至兼容性视图
3. 当使用兼容性视图浏览时，网页呈现的效果与实际浏览器文档渲染标准不符，导致出现兼容性问题。

##兼容性视图
> 兼容性视图是微软为了兼容基于其它网页标准开发的网站，确保浏览者在浏览网页时不至于受困于网页显示混乱的问题，而专门为IE8增加的一项功能。 

##文档模式
> 当IE8检测到某网站不兼容时，点击地址栏右侧出现的兼容性视图按钮，或者页面自动刷新转换为兼容性视图，最终将网页的文档模式从 W3C标准 转换为 兼容性模式 。

1. **W3C标准** 
默认情况下，IE8的文档模式就是IE8，其已经全面支持 [W3C](http://www.chinaw3c.org/standards.html) 制定的标准，包括结构(`XHTML 1.0`)，样式(`CSS 2`)，行为(`DOM,ECMAScript`)

2. **兼容性模式**
IE8兼容性模式是IE7文档模式，该标准只是在IE6的基础上修复了一些常见Bug，还不能完全支持W3C标准  [参考](http://www.blueidea.com/tech/web/2008/6100.asp)

##解决方案
-   目前Web编码规范严格按照W3C标准执行，不需要切换至兼容性视图模式来解析网页；
-   客户端的IE兼容性视图设置，需要移除兼容性视图来进行浏览网站；
- 最终想要解决这个问题，需要开发者和客户端一起来控制，具体操作如下：

**开发者**
1.  在每个 HTML 页面开头使用这个doctype 来启用标准模式，使其每个浏览器保持展现一致
```
<!DOCTYPE html>
<html>
        <head>
        </head>
</html>
```
2. 禁止在doctype之前加入HTML注释，此操作会触发浏览器的怪异模式

```
<!-- Author:jobs-->
<!DOCTYPE html>
```
3. 在页面中定义文档兼容性模式，让IE始终按照当前网站的兼容版本(IE8)或者浏览器最高版本解析网页
**兼容版本(IE8)**
```
<!DOCTYPE html>
<html lang="zh-CN">
    <head>
        <title>pageTitle</title>
    	<meta http-equiv="content-type" content="text/html;charset=utf-8">
    	<meta http-equiv="X-UA-Compatible" content="IE=Edge">
    	<link rel="stylesheet" type="text/css" href="css.css">
    </head>
    <body></body>
</html>
```
**最高版本**
```
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```
`X-UA-compatible`除了`title`元素及其他的`meta`元素之外，它必须放在网页`head`节点内其它元素之前的位置

**客户端**
1. 打开IE - 工具 - 兼容性视图设置
2. 删除 - 兼容性视图中的 IP 或 网址
3. 勾掉 - 最下面三个选项前面的勾
4. 关闭

##更新
- qijc@asiainfo.com 2014-08-07
- qifei3@asiainfo.com / 2014-08-05
