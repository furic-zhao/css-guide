## CSS开发规范
### 基本语法
- 用两个空格来代替制表符（tab） -- 这是唯一能保证在所有环境下获得一致展现的方法。
- 为选择器分组时，将单独的选择器单独放在一行。
- 为了代码的易读性，在每个声明块的左花括号前添加一个空格。
- 声明块的右花括号应当单独成行。
- 每条声明语句的 `:` 后应该插入一个空格。
- 为了获得更准确的错误报告，每条声明都应该独占一行。
- 所有声明语句都应当以分号结尾。最后一条声明语句后面的分号是可选的，但是，如果省略这个分号，你的代码可能更易出错。
- 对于以逗号分隔的属性值，每个逗号后面都应该插入一个空格（例如，`box-shadow`）。
- 不要在 `rgb()`、`rgba()`、`hsl()`、`hsla()` 或 `rect()` 值的内部的逗号后面插入空格。这样利于从多个属性值（既加逗号也加空格）中区分多个颜色值（只加逗号，不加空格）。
- 对于属性值或颜色参数，省略小于 1 的小数前面的 0 （例如，`.5` 代替 `0.5`；`-.5px` 代替 `-0.5px`）。
- 十六进制值应该全部小写，例如，`#fff`。在扫描文档时，小写字符易于分辨，因为他们的形式更易于区分。
- 尽量使用简写形式的十六进制值，例如，用 `#fff` 代替 `#ffffff`。
- 为选择器中的属性添加双引号，例如，`input[type="text"]`。[只有在某些情况下是可选的](https://mathiasbynens.be/notes/unquoted-attribute-values#css)，但是，为了代码的一致性，建议都加上双引号。
- 避免为 0 值指定单位，例如，用 `margin: 0;` 代替 `margin: 0px;`。
对于这里用到的术语有疑问吗？请参考 Wikipedia 上的 [syntax section of the Cascading Style Sheets article](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax)。

```
/* Bad CSS */
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

/* Good CSS */
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgba(0,0,0,.5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```
### 命名规范

**组成元素**
- 命名必须由单词、中划线或数字组成；
- 不允许使用拼音（约定俗成的除外，如：youku, baidu），尤其是缩写的拼音、拼音与英文的混合。

```
/* Bad example */
.xiangqing { sRules; }
.news_list { sRules; }
.zhuti { sRules; }

/* Good example */
.detail { sRules; }
.news-list { sRules; }
.topic { sRules; }

```

> 我们使用中划线 `-` 作为连接字符，而不是下划线 `_`。 `-` 能让你少按一次shift键，并且更符合CSS原生语法，所以我们只选一种目前业内普遍使用的方式

**词汇规范**
- 不依据表现形式来命名；
- 可根据内容来命名；
- 可根据功能来命名。

```
/* Bad example */
left, right, center, red, black

/* Good example */
nav, aside, news, type, search
```

**缩写规范**
保证缩写后还能较为清晰保持原单词所能表述的意思；
使用业界熟知的或者约定俗成的。

```
/* Bad example */
navigation   =>  navi
header       =>  head
description  =>  des

/* Good example */
navigation   =>  nav
header       =>  hd
description  =>  desc
```

**前缀规范**

|前缀|说明|示例|
|---|---|---|
|g-	|全局通用样式命名，前缀g全称为global，一旦修改将影响全站样式	|g-mod|
|m-	|模块命名方式	|m-detail|
|ui-|组件命名方式	|ui-selector|
|js-|所有用于纯交互的命名，不涉及任何样式规则。JSer拥有全部定义权限|js-switch|

```
/* Bad example */
.info { sRules; }
.current { sRules; }
.news { sRules; }

/* Good example */
.m-detail .info { sRules; }
.m-detail .current { sRules; }
.m-detail .news { sRules; }
```

> 不好的命名规则给我们带来不可预知的管理麻烦以及沉重的历史包袱。你永远也不会知道哪些样式名已经被用掉了，如果你是一个新人，你可能会遭遇，你每定义个样式名，都有同名的样式已存在，然后你只能是换样式名或者覆盖规则。

### 常用CSS命名

|中文名	|建议类名|	中文名|建议类名|
|--|--|--|--|
|头部	|header	|外围容器|	wrapper|
|尾部	|footer	|容器|	container|
|内容	|content|	页面主体|	main|
|导航	|nav|	栏目/列|	column|
|顶导航	|topnav|	菜单|	menu|
|子导航	|subnav|	侧栏|	sidebar|
|子菜单	|submenu|	模块|	module|
|标题	|title|	标签页|	tab|
|小技巧	|tips|	状态|	status|
|提示信息	|msg|	按钮|	btn|
|摘要	|summary|	购物车/收银台|	shop|
|注释	|note|	搜索|	search|
|结果	|result|	排序|	sort|
|价格	|price|	滚动|	scroll|
|下拉	|drop-down|	当前|	current|

### 声明顺序
相关的属性声明应当归为一组，并按照下面的顺序排列
1. Positioning
2. Box model
3. Typographic
4. Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

完整的属性列表及其排列顺序请参考 [Recess](http://twitter.github.io/recess/)。

```
.declaration-order {
  /* Positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  /* Box-model */
  display: block;
  float: right;
  width: 100px;
  height: 100px;

  /* Typography */
  font: normal 13px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;

  /* Visual */
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  /* Misc */
  opacity: 1;
}
```

### 不要使用 @import
与 `<link>` 标签相比，`@import`指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法有以下几种：

- 使用多个 `<link>` 元素
- 通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件
- 通过 Rails、Jekyll 或其他系统中提供过 CSS 文件合并功能
请参考 [Steve Souders](http://www.stevesouders.com/blog/2009/04/09/dont-use-import/) 的文章了解更多知识。

```
<!-- Use link elements -->
<link rel="stylesheet" href="core.css">

<!-- Avoid @imports -->
<style>
  @import url("more.css");
</style>
```

### 媒体查询（Media query）的位置
将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。下面给出一个典型的实例。

```
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

### 带前缀的属性
当使用特定厂商的带有前缀的属性时，通过缩进的方式，让每个属性的值在垂直方向对齐，这样便于多行编辑。

在 Textmate 中，使用 `Text → Edit Each Line in Selection (⌃⌘A)`。在 Sublime Text 2 中，使用 `Selection → Add Previous Line (⌃⇧↑)` 和 `Selection → Add Next Line (⌃⇧↓)`。

```
/* Prefixed properties */
.selector {
  -webkit-box-shadow: 0 1px 2px rgba(0,0,0,.15);
          box-shadow: 0 1px 2px rgba(0,0,0,.15);
}
```

### 单行规则声明
对于只包含一条声明的样式，为了易读性和便于快速编辑，建议将语句放在同一行。对于带有多条声明的样式，还是应当将声明分为多行。

> 这样做的关键因素是为了错误检测 -- 例如，CSS 校验器指出在 183 行有语法错误。如果是单行单条声明，你就不会忽略这个错误；如果是单行多条声明的话，你就要仔细分析避免漏掉错误了。

```
/* Single declarations on one line */
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

/* Multiple declarations, one per line */
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url(../img/sprite.png);
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
```

### 简写形式的属性声明
在需要显示地设置所有值的情况下，应当尽量限制使用简写形式的属性声明。常见的滥用简写属性声明的情况如下：

- padding
- margin
- font
- background
- border
- border-radius
大部分情况下，我们不需要为简写形式的属性声明指定所有值。例如，HTML 的 heading 元素只需要设置上、下边距（margin）的值，因此，在必要的时候，只需覆盖这两个值就可以。过度使用简写形式的属性声明会导致代码混乱，并且会对属性值带来不必要的覆盖从而引起意外的副作用。

在 MDN（Mozilla Developer Network）上一篇非常好的关于[shorthand properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties) 的文章，对于不太熟悉简写属性声明及其行为的用户很有用。

```
/* Bad example */
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

/* Good example */
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

### Less 和 Sass 中的嵌套
避免不必要的嵌套。这是因为虽然你可以使用嵌套，但是并不意味着应该使用嵌套。只有在必须将样式限制在父元素内（也就是后代选择器），并且存在多个需要嵌套的元素时才使用嵌套。

扩展阅读：
[Nesting in Sass and Less](http://markdotto.com/2015/07/20/css-nesting/)

```
// Without nesting
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// With nesting
.table > thead > tr {
  > th { … }
  > td { … }
}
```

### Less 和 Sass 中的操作符
为了提高可读性，在圆括号中的数学计算表达式的数值、变量和操作符之间均添加一个空格。

```
// Bad example
.element {
  margin: 10px 0 @variable*2 10px;
}

// Good example
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

### 注释
代码是由人编写并维护的。请确保你的代码能够自描述、注释良好并且易于他人理解。好的代码注释能够传达上下文关系和代码目的。不要简单地重申组件或 class 名称。

**普通注释(单行)**

```
/* 普通注释 */
```

**区块注释**

```
/**
* @description: 文件中文说明
* @author: yourname
* @update: yourname (2015-05-29 18:32)
*/
```

**特殊注释**

```
用于标注代办、修改等信息
/* TODO: xxxx by yourname 2015-05-29 18:32 */
/* BUGFIX: xxxx by yourname 2015-05-29 18:32 */
```

> 有特殊作用的规则一定要有注释说明 应用了高级技巧的地方一定要注释说明

```
/* Bad example */
/* Modal header */
.modal-header {
  ...
}

/* Good example */
/* Wrapping element for .modal-title and .modal-close */
.modal-header {
  ...
}
```

> 对于较长的注释，务必书写完整的句子；对于一般性注解，可以书写简洁的短语。

### class 命名
- class 名称中只能出现小写字符和破折号（dashe）（不是下划线，也不是驼峰命名法）。破折号应当用于相关 class 的命名（类似于命名空间）（例如，.btn 和 .btn-danger）。
- 避免过度任意的简写。.btn 代表 button，但是 .s 不能表达任何意思。
- class 名称应当尽可能短，并且意义明确。
- 使用有意义的名称。使用有组织的或目的明确的名称，不要使用表现形式（presentational）的名称。
- 基于最近的父 class 或基本（base） class 作为新 class 的前缀。
- 使用 .js-* class 来标识行为（与样式相对），并且不要将这些 class 包含到 CSS 文件中。

> 在为 Sass 和 Less 变量命名时也可以参考上面列出的各项规范。

```
/* Bad example */
.t { ... }
.red { ... }
.header { ... }

/* Good example */
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

### 选择器
- 对于通用元素使用 class ，这样利于渲染性能的优化。
- 对于经常出现的组件，避免使用属性选择器（例如，[class^="..."]）。浏览器的性能会受到这些因素的影响。
- 选择器要尽可能短，并且尽量限制组成选择器的元素个数，建议不要超过 3 。
- 只有在必要的时候才将 class 限制在最近的父元素内（也就是后代选择器）（例如，不使用带前缀的 class 时 -- 前缀类似于命名空间）。

更多参考：
[Scope CSS classes with prefixes](http://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
[Stop the cascade](http://markdotto.com/2012/03/02/stop-the-cascade/)

```
/* Bad example */
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

/* Good example */
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

### 代码组织
- 以组件为单位组织代码段。
- 制定一致的注释规范。
- 使用一致的空白符将代码分隔成块，这样利于扫描较大的文档。
- 如果使用了多个 CSS 文件，将其按照组件而非页面的形式分拆，因为页面会被重组，而组件只会被移动。

```
/*
 * Component section heading
 */

.element { ... }


/*
 * Component section heading
 *
 * Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
 */

.element { ... }

/* Contextual sub-component or modifer */
.element-heading { ... }
```

### CSS模块化

- 每个模块必须是一个独立的样式文件，文件名与模块名一致。
- 模块样式的选择器必须以模块名开头以作范围约定。

```
.m-detail {
	background: #fff;
	color: #333;
	&-hd {
		padding: 5px 10px;
		background: #eee;
		.title {
			background: #eee;
		}
	}
	&-bd {
		padding: 10px;
		.info {
			font-size: 14px;
			text-indent: 2em;
		}
	}
	&-ft {
		text-align: center;
		.more {
			color: blue;
		}
	}
}
```

```
.m-detail {
	background: #fff;
	color: #333;
}
.m-detail-hd {
	padding: 5px 10px;
	background: #eee;
}
.m-detail-hd .title {
	background: #eee;
}
.m-detail-bd {
	padding: 10px;
}
.m-detail-bd .info {
	font-size: 14px;
	text-indent: 2em;
}
.m-detail-ft {
	text-align: center;
}
.m-detail-ft .more {
	color: blue;
}
```

> 为了提高CSS解析性能，任何超过3级的选择器，需要思考是否必要，是否有无歧义的，能唯一命中的更简短的写法

### 编辑器配置
将你的编辑器按照下面的配置进行设置，以避免常见的代码不一致和差异：

- 用两个空格代替制表符（soft-tab 即用空格代表 tab 符）。
- 保存文件时，删除尾部的空白符。
- 设置文件编码为 UTF-8。
- 在文件结尾添加一个空白行。
参照文档并将这些配置信息添加到项目的 `.editorconfig` 文件中。例如：[FEZ 中的 .editorconfig 实例](https://github.com/furic-zhao/fez/blob/master/.editorconfig)。更多信息请参考 [about EditorConfig](http://editorconfig.org/)。
