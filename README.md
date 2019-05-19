# 数字漫画协会 EPUB3 固定布局 规格指南 ver.1.0

デジタルコミック協議会 EPUB3 固定レイアウト 仕様ガイド ver.1.0 [原文 PDF](http://www.digital-comic.jp/press_release_DCA_EPUB3.pdf)

2012/11/22

--------

**— Work In Progress —**



本指南是用于漫画内容制作开发和阅读系统（RS）的 EPUB3 固定布局规范。 目前，IDPF（[国际数字出版论坛](https://zh.wikipedia.org/w/index.php?title=國際數位出版論壇&action=edit&redlink=1) [International Digital Publishing Forum](http://idpf.org/)）指定的 EPUB3 规范中国允许各种各样的表述，因此制作出来的文件存在差异差别很大，并且存在阅读系统不能顺利{再現 渲染？}的情况。本指南的使用能促进数字漫画的创作和发布，并希望在更多的电子书店中提供更多的漫画，读者也能获得丰富的阅读体验。

## 1. 基本的目录结构和文件名

```bash
root 文件夹
├── mimetype
├── META-INF 文件夹
│   └── container.xml
└── item 文件夹
    ├── standard.opf
    ├── navigation-documents.xhtml
    ├── image 文件夹
    ├── style 文件夹
    └── xhtml 文件夹
```

* root 文件夹的名字根据版本说明而定

* 文件和文件夹的名字原则上使用小写字母（META_INF 和 { ? // TODO } 除外）

* 根据包文档中的 `<item>` 标签，资源文件夹的名字应该为 item（规范允许任意名字）
* 所有的资源文件应该放在 item 目录下的指定文件夹里：

  图片文件			：image 文件夹

  CSS 样式文件	：style 文件夹

  xhtml 文件		：xhtml 文件夹

* 以下文件中的每一个字符都不要修改：

  root 目录下的 mimetype

  META_INF 目录下的 container.xml

  

## 2. 文件规范

* 根据底稿中的每一个文件进行分页分割到新创建的 xhtml 文件

* 该文件的标题基于该作品的标题

  在 xhtml 文档中 `<title>` 标签的内容，除非出版商有特别规定的情况，都应该填上作品的标题。{稍后会使用到包文档（opf 文件）的作品名信息。?}使用全角空格符号连接主标题、副标题和系列名称。在内容不一样的情况，例如一个内容中包含有多个作品的合集作品，则使用出版商指定的名字。

* 只在封面和导航文档中插入 epub:type

  在 EPUB 中，可以定义名为 epub:type 的属性来指定页面的作用。{但是，目前没有使用这个属性的 RS 并不能保证能利用 // TODO }。因此，目前仅指定将来系统可能会使用到的两个地方。

  封面图片页面 `<body epub:type="cover" class="p-cover">`

  导航文件 `<nav epub:type="toc" id="toc">`



## 3. 简单的编码规则

* 字符编码推荐 UTF-8N（无BOM）
* 换行符不要混合在同一个文件中
* 不推荐使用本指南中没有涉及到的 html 标签和 css 属性
* 请不要在原始底本指定之外的地方插入评论注释
* 本文内标签属性的描述顺序为：`epub:type` → `class` → `id` → `src/href` → `alt`
* 为了避免混乱，`<p>` 标签应该尽可能少加 class 属性
* 在 xhtml 文档中的 html 标签之后进行换行

对于块级元素（如 `<div>`），请确保开始标签和结束标签前后要进行换行。但是，对于 `<p>` 标签和 `<h1>` - `<h6>` 标签，请不要在开始标签和结束标签之前进行换行。

```html
<!-- 错误的标签换行 -->
<h1>
テキスト
</h1>
<div><p>テキスト</p></div>

<!-- 正确的标签换行 -->
<h1>テキスト</h1>
<div>
 <p>テキスト</p>
</div>
```

对于内联元素（如 \<span\>），原则上避免换行。对于 \<a\> 标签的情况，除非 \<a\> 标签中包含块级元素（包括 \<p\>）或 \<img\>，否则不要进行换行。


