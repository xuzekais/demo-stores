# demo-stores

# 1.多行文本溢出显示省略号

#### tips:
1.实现最简单的单行文本溢出省略号
2.实现多行文本溢出省略号
3.多行文本遇到数字和英文提前省略的解决方法

### 实现最简单的单行文本溢出省略号

```css
 .text{
 	overflow: hidden;
 	white-space: nowrap;
	text-overflow: ellipsis;
}
```
这是较为基础的写法
### 实现多行文本溢出省略号
在WebKit浏览器或移动端（绝大部分是WebKit内核的浏览器）的页面实现比较简单，可以直接使用WebKit的CSS扩展属性(WebKit是私有属性)-webkit-line-clamp ；注意：这是一个 不规范的属性（unsupported WebKit property），它没有出现在 CSS 规范草案中。

-webkit-line-clamp用来限制在一个块元素显示的文本的行数。 为了实现该效果，它需要组合其他的WebKit属性。查看 text-overflow 属性文档：https://www.html.cn/book/css/webkit/text/line-clamp.htm

常见结合属性：

display: -webkit-box; 必须结合的属性 ，将对象作为弹性伸缩盒子模型显示 。

-webkit-box-orient 必须结合的属性 ，设置或检索伸缩盒对象的子元素的排列方式 。

text-overflow: ellipsis;，可以用来多行文本的情况下，用省略号“…”隐藏超出范围的文本 。查看 `text-overflow` 属性文档：https://www.html.cn/book/css/properties/user-interface/text-overflow.htm


```css
.text{
	overflow : hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
}
```


这个属性比较合适WebKit浏览器或移动端（绝大部分是WebKit内核的）浏览器。

具体例子可以查看https://www.html.cn/book/css/webkit/text/line-clamp.htm

###  多行文本遇到数字和英文提前省略的解决方法
例如：
![](https://img-blog.csdnimg.cn/20210519230923461.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjc1NzgxMg==,size_16,color_FFFFFF,t_70)
首先按照上面代码将-webkit-line-clamp设置为2，意味着我们想要他两行的时候溢出省略但是效果和我们想象的不一样

接着我们看一下文本信息
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210519231148138.png)
我们可以看到实际上后面还有很多文字只不过在遇到文字AAAAAAAAAAAAAAAAAA之后被提前省略了

```css
.text{
	overflow : hidden;
	text-overflow: ellipsis;
	display: -webkit-box;
	-webkit-line-clamp: 2;
	-webkit-box-orient: vertical;
	/* 新加一个*/
	word-break: break-all;
}
```
[word-break](https://www.w3school.com.cn/cssref/pr_word-break.asp)它的默认值为：normal，意味着使用浏览器的换行规则，但是当它设置为break-all为：允许在单词内换行。

最后我们看一下效果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20210519231516123.png)