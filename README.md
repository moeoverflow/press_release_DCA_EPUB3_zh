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



## 4. epub 的配置文件模板列表

* 模板和文件的命名规则

除非另有说明，否则请使用以下模板和文件名规定。 如果您需要除此处列出的模板或文件名规定之外的模板或文件名规定，则由每个出版商给出说明。

* 源（文本）的整理规范

关于源的格式，例如源中的换行符和缩进，以及元素中的标签属性顺序，遵循（本指南？）每个版本的说明。 除非另有说明，否则请根据以下模板进行整理规范格式化。

* 关于模板中的颜色编码

<span style="color: #808080;">灰色</span>：所有作品共有的部分（原则上不更改）

<span style="color: #0005ff;">蓝色</span>：在所有作品共有的部分中，每个作品需要单独更改的部分

<span style="color: #ff0000;">红色</span>：该模板所特有、应该注意的部分（原则上不更改）

<span style="color: black;">黑色</span>：不固定的部分（因作品和出版商而异）

#### 4-1: mimetype

------

<div><p><span style="color:#6d6d6d">application/epub+zip</span></p></div>

--------



#### 4-2: container.xml

* 放在 META-INF 文件夹中

-------

<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;container</span></p><p><span style="color:#6d6d6d">&nbsp; version="1.0"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="urn:oasis:names:tc:opendocument:xmlns:container" &gt; </span></p><p><span style="color:#6d6d6d">&lt;rootfiles&gt;</span></p><p><span style="color:#6d6d6d">&lt;rootfile</span></p><p><span style="color:#6d6d6d">&nbsp; full-path="item/standard.opf"</span></p><p><span style="color:#6d6d6d">&nbsp; media-type="application/oebps-package+xml" /&gt;</span></p><p><span style="color:#6d6d6d">&lt;/rootfiles&gt;</span></p><p><span style="color:#6d6d6d">&lt;/container&gt; </span></p></div>

-------



#### 4-3: standard.opf

* 如果阅读系统具有显示 `<dc:title>` 信息的功能，请假设所有的这些内容会被阅读系统显示在屏幕的某处。

* 如果阅读系统具有显示 `<dc:creator>` 信息的功能，并且可能有多个 `<dc:creator>` 的情况 ，请假设所有的这些内容会被阅读系统显示在屏幕的某处。（用于链接多个作者姓名和显示角色注解的符号应由阅读系统自行决定。）

* 是逐个划分多个作者姓名到多个 `<dc:creator>` 还是将它们全部列在同一个 `<dc:creator>` 中，请遵循出版商的说明。 在分多个标签的情况下，应由出版商指定每个作者的“角色”值（「role」の値）和显示顺序。

* 假定由 `file-as` 指定的排列用假名不会显示在读者的阅读器上。

* 文件ID（unique-identifier）的编码方案没有明确的（格式？）要求，由出版商决定。除非另有说明，否则请一定要插入 uuid。

* 除非另有说明，否则更新日期将是计划的交付日期，以方便文件管理。

* 更新日期不会显示给读者。

* 除非另有说明，否则封面图像的文件名是同意的名字（cover.jpg），用于加速阅读系统的缩略图显示。

* 对于左开式作品的情况，`<spine>` 的 `page-progression-direction` 由 `rtl` 改为 `ltr`。

* 在 `<spine>` 的 `<itemref>` 中，如果存在重复的 idref 值，则不会显示任何内容（Readium）或者如果页面循环（Firefox 的 EPUBReader），则相同的图像将会显示两次。 如果你想显示更多，以防万一建议准备一个单独的 xhtml 文件来调用图像（例如，white2.xhtml 为第二个白色图像）

* 与日本電子書籍出版社協会（電書協）的 EPUB3 （）回流型指南的不同之处有以下几点：

  ◇ `<package>` 标签追加 prefix 属性

  ◇ `<!-- Fixed-Layout Documents指定 -->` 部分追加两个 `<meta>` 标签

  ◇ 样式表只有 fixed-layout-jp.css

  ◇ 才用 SVG 的封装方法。SVG 直接嵌入 xhtml 文档中。考虑到一些不支持 svg 的阅读系统，在 `<item>` 的 xhtml 文件中的添加相应的图片作为备选

  ◇ 将 `properties ="rendition: page-spread-center"`添加到 `<spine>` 中的 `<itemref>` 封面页

--------

<div style="font-size: 14px;"><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;package </span></p><p><span>&nbsp; </span><span style="color:#6d6d6d">xmlns="http://www.idpf.org/2007/opf"</span></p><p><span style="color:#6d6d6d">&nbsp; version="3.0"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&nbsp; unique-identifier="</span><span style="color:#0000ff">unique-id</span><span style="color:#6d6d6d">"</span></p><p><span style="color:#6d6d6d">&nbsp; </span><span style="color:#fb0007">prefix="rendition: http://www.idpf.org/vocab/rendition/#ebpaj: http://www.ebpaj.jp/"</span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&lt;metadata xmlns:dc="http://purl.org/dc/elements/1.1/"&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">作品名</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:title id="title"&gt;</span><span style="color:#0000ff">作品名</span><span style="color:#0000ff">1</span><span style="color:#6d6d6d">&lt;/dc:title&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#title" property="file-as"&gt;</span><span style="color:#0000ff">セイレツヨウサクヒンメイカナ</span><span style="color:#0000ff">01</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">著者名</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:creator id="</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">"&gt;</span><span style="color:#0000ff">著作者名</span><span style="color:#0000ff">1</span><span style="color:#6d6d6d">&lt;/dc:creator&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">" property="role" scheme="marc:relators"&gt;</span><span style="color:#0000ff">aut</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">" property="file-as"&gt; </span><span style="color:#0000ff">セ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">レ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ツ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ヨ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ウ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">チ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ョ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">サ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ク</span><span style="color:#0000ff"> </span><span style="color:#0000ff">シ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ャ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">メ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">カ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ナ</span><span style="color:#0000ff"> 01</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">" property="display-seq"&gt;</span><span style="color:#0000ff">1</span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;dc:creator id="</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">"&gt;</span><span style="color:#0000ff">著作者名</span><span style="color:#0000ff">2</span><span style="color:#6d6d6d">&lt;/dc:creator&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">" property="role" scheme="marc:relators"&gt;</span><span style="color:#0000ff">aut</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">" property="file-as"&gt; </span><span style="color:#0000ff">セ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">レ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ツ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ヨ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ウ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">チ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ョ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">サ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ク</span><span style="color:#0000ff"> </span><span style="color:#0000ff">シ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ャ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">メ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">カ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ナ</span><span style="color:#0000ff"> 02</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">" property="display-seq"&gt;</span><span style="color:#0000ff">2</span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">出版社名</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:publisher id="publisher"&gt;</span><span style="color:#0000ff">出版社名</span><span style="color:#6d6d6d">&lt;/dc:publisher&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#publisher" property="file-as"&gt;</span><span style="color:#0000ff">セイレツヨウシュッハ</span><span style="color:#0000ff">゚ンシャメイカナ</span><span style="color:#0000ff"> </span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">言語</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:language&gt;ja&lt;/dc:language&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">ファイル</span><span style="color:#6d6d6d">id --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:identifier id="</span><span style="color:#0000ff">unique-id</span><span style="color:#6d6d6d">"&gt;</span><span style="color:#0000ff">urn:uuid:860ddf31-55a4-449a-8cc9-3c1837657a15</span><span style="color:#6d6d6d">&lt;/dc:identifier&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">更新日</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="dcterms:modified"&gt;</span><span style="color:#0000ff">2012-01-01T00:00:00Z</span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- Fixed-Layout Documents</span><span style="color:#6d6d6d">指定</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#fb0007">&lt;meta property="rendition:layout"&gt;pre-paginated&lt;/meta&gt;</span></p><p><span style="color:#fb0007">&lt;meta property="rendition:spread"&gt;landscape&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- etc. --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="ebpaj:guide-version"&gt;1.1&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;/metadata&gt;</span></p><p><span style="color:#6d6d6d">&lt;manifest&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- navigation --&gt; </span></p><p><span style="color:#6d6d6d">&lt;item media-type="application/xhtml+xml" id="</span><span style="color:#0000ff">toc</span><span style="color:#6d6d6d">" href="</span><span style="color:#0000ff">navigation-documents.xhtml</span><span style="color:#6d6d6d">" </span><span style="color:#fb0007">properties="nav"</span><span style="color:#6d6d6d">/&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- style --&gt;</span></p><p><span style="color:#6d6d6d">&lt;item media-type="text/css" id="</span><span style="color:#fb0007">fixed-layout-jp</span><span style="color:#6d6d6d">" href="style/</span><span style="color:#fb0007">fixed-layout-jp.css</span><span style="color:#6d6d6d">"/&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- image --&gt;</span></p><p><span style="color:#6d6d6d">&lt;item media-type="image/</span><span style="color:#0000ff">jpeg</span><span style="color:#6d6d6d">" id="cover" </span><span>href="image/cover.</span><span style="color:#0000ff">jpg</span><span>"</span><span style="color:#6d6d6d"> </span><span style="color:#fb0007">properties="cover-image"</span><span style="color:#6d6d6d">/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-white" href="image/i-white.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-001" href="image/i-001.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-002" href="image/i-002.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-003" href="image/i-003.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-004" href="image/i-004.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-005" href="image/i-005.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-colophon" href="image/i-colophon.jpg"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- xhtml --&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-cover" </span><span>href="image/cover.jpg"</span><span> </span><span style="color:#fb0007">properties="svg" fallback="cover"</span><span>/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-white" href="xhtml/p-white.xhtml" properties="svg" fallback="i-white"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-001" href="xhtml/p-001.xhtml" properties="svg" fallback="i-001"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-002" href="xhtml/p-002.xhtml" properties="svg" fallback="i-002"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-003" href="xhtml/p-003.xhtml" properties="svg" fallback="i-003"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-004" href="xhtml/p-004.xhtml" properties="svg" fallback="i-004"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-005" href="xhtml/p-005.xhtml" properties="svg" fallback="i-005"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-colophon" href="xhtml/p-colophon.xhtml" properties="svg" fallback="i-colophon"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-white2" href="xhtml/p-white2.xhtml" properties="svg" fallback="i-white"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/manifest&gt;</span></p><p><span style="color:#6d6d6d">&lt;spine page-progression-direction="</span><span style="color:#0000ff">rtl</span><span style="color:#6d6d6d">"&gt; </span></p><p><span>&lt;itemref linear="yes" idref="p-cover" properties="</span><span style="color:#fb0207">rendition:page-spread-center</span><span>"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-white" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-001" properties="page-spread-left"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-002" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-003" properties="page-spread-left"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-004" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-005" properties="page-spread-left"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-colophon" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-white2" properties="page-spread-left"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/spine&gt;</span></p><p><span style="color:#6d6d6d">&lt;/package&gt;</span></p></div>

---------



<参考信息>

为了使页面快速地适配并显示所有页面固定大小的图像，建议在描述 OPF 文件中的标准大小时进行如下描述：

* 给 <package> 标签追加 prefix 描述
* 将页面图像标准大小规范添加到 `<metadata>`
* 所有页面图像的尺寸应该相同，原始图像的垂直和水平px值在下文的蓝色部分中指定

-------
<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;package</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="http://www.idpf.org/2007/opf"</span></p><p><span style="color:#6d6d6d">&nbsp; version="3.0"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&nbsp; unique-identifier="unique-id"</span></p><p><span style="color:#6d6d6d">&nbsp; prefix="rendition: http://www.idpf.org/vocab/rendition/# </span></p><p><span style="width:36pt; display:inline-block">&nbsp;</span><span style="color:#6d6d6d">&nbsp;&nbsp;&nbsp; ebpaj: http://www.ebpaj.jp/ </span></p><p><span style="color:#fb0007">&nbsp; </span><span style="width:29.5pt; display:inline-block">&nbsp;</span><span style="color:#fb0007">&nbsp;&nbsp;&nbsp; fixed-layout-jp: http://www.digital-comic.jp/</span><span style="font-size:13pt">" </span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;metadata xmlns:dc="http://purl.org/dc/elements/1.1/"&gt; </span></p><p><span>&nbsp;</span></p><p style="text-align:center; "><span style="color:#fb0007">(</span><span style="color:#fb0007">※</span><span style="color:#fb0007">中略</span><span style="color:#fb0007">) </span></p><p><span>&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;!-- Fixed-Layout Documents</span><span style="color:#6d6d6d">指定</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="rendition:layout"&gt;pre-paginated&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="rendition:spread"&gt;landscape&lt;/meta&gt; </span></p><p><span>&nbsp;</span></p><p><span style="color:#fb0007">&lt;!-- </span><span style="color:#fb0007">基準サイス</span><span style="color:#fb0007">゙</span><span style="color:#fb0007"> --&gt;</span></p><p><span style="color:#fb0007">&lt;meta property="fixed-layout-jp:viewport"&gt;width=</span><span style="color:#0000ff">848</span><span style="color:#fb0007">, height=</span><span style="color:#0000ff">1200</span><span style="color:#fb0007">&lt;/meta&gt;</span></p><p><span style="color:#fb0007">&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;!-- etc. --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="ebpaj:guide-version"&gt;1.1&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;/metadata&gt;</span></p><p><span>&nbsp;</span></p><p style="text-align:center; "><span style="color:#fb0007">(</span><span style="color:#fb0007">※</span><span style="color:#fb0007">後略</span><span style="color:#fb0007">) </span></p></div>

-------

#### 4-4: navigation-documents.xhtml

* 链接项和列表的层次结构根据作品内容而变化
* 除非出版商另有指示，否则仅链接到封面，TOC 页面和版本说明页面
* 本规范不支持在导航文档中包含非链接项目
* 显示导航文档方式实现留给阅读系统
* 当导航文档也被显示为文本中的目录页面时，将参考稍后描述的文本页面等的示例插入样式表规范等。XXX
* 如果文件名是序号类型的，请作相应调整（在下面的示例中，目录为 p-001.xhtml）

------

<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;!DOCTYPE html&gt;</span></p><p><span style="color:#6d6d6d">&lt;html</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="http://www.w3.org/1999/xhtml"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:epub="http://www.idpf.org/2007/ops"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&lt;head&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta charset="UTF-8"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;title&gt;</span><span style="color:#0000ff">Navigation</span><span style="color:#6d6d6d">&lt;/title&gt;</span></p><p><span style="color:#6d6d6d">&lt;/head&gt;</span></p><p><span style="color:#6d6d6d">&lt;body&gt;</span></p><p><span style="color:#6d6d6d">&lt;nav </span><span style="color:#fb0007">epub:type="toc" id="toc"</span><span style="color:#6d6d6d">&gt; &lt;h1&gt;</span><span style="color:#0000ff">Navigation</span><span style="color:#6d6d6d">&lt;/h1&gt;</span></p><p><span style="color:#6d6d6d">&lt;ol&gt;</span></p><p><span>&lt;li&gt;&lt;a href="xhtml/p-cover.xhtml"&gt;</span><span>表紙</span><span>&lt;/a&gt;&lt;/li&gt;</span></p><p><span>&lt;li&gt;&lt;a href="xhtml/p-001.xhtml"&gt;</span><span>目次</span><span>&lt;/a&gt;&lt;/li&gt;</span></p><p><span>&lt;li&gt;&lt;a href="xhtml/p-colophon.xhtml"&gt;</span><span>奥付</span><span>&lt;/a&gt;&lt;/li&gt;</span></p><p><span style="color:#6d6d6d">&lt;/ol&gt;</span></p><p><span style="color:#6d6d6d">&lt;/nav&gt;</span></p><p><span style="color:#6d6d6d">&lt;/body&gt;</span></p><p><span style="color:#6d6d6d">&lt;/html&gt; </span></p></div>

--------



## 4-5: XHTML 文档文件

* 封面页面 [cover.xhtml]

  以下三个位置以蓝色列出图像的原始大小

--------

<div><p style=""><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;!DOCTYPE html&gt;</span></p><p style=""><span style="milyfont-fa:Times-Roman; color:#6d6d6d">&lt;html</span></p><p style=""><span style="color:#6d6d6d">&nbsp; xmlns="http://www.w3.org/1999/xhtml"</span></p><p style=""><span style="color:#6d6d6d">&nbsp; xmlns:epub="http://www.idpf.org/2007/ops"</span></p><p style=""><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p style=""><span style="color:#6d6d6d">&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;head&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;meta charset="UTF-8"/&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;title&gt;</span><span style="color:#0000ff">作品名</span><span style="color:#6d6d6d">&lt;/title&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;link rel="stylesheet" type="text/css" href="../style/</span><span style="color:#fb0007">fixed-layout-jp.css</span><span style="color:#6d6d6d">"/&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;meta name="viewport" content="width=</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">, height=</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">"/&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;/head&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;body </span><span style="color:#fb0007">epub:type="cover"</span><span style="color:#6d6d6d">&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;div class="main"&gt;</span></p><p style=""><span style="font-size:12pt">&nbsp;</span></p><p style=""><span style="color:#6d6d6d">&lt;svg xmlns="http://www.w3.org/2000/svg" version="1.1"</span></p><p style=""><span style="color:#6d6d6d">&nbsp; xmlns:xlink="http://www.w3.org/1999/xlink"</span></p><p style=""><span style="color:#6d6d6d">&nbsp; width="100%" height="100%" viewBox="0 0 </span><span style="color:#0000ff">848 1200</span><span style="color:#6d6d6d">"&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;image width="</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">" height="</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">" xlink:href="../image/</span><span style="color:#fb0007">cover.jpg</span><span style="color:#6d6d6d">"/&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;/svg&gt;</span></p><p style=""><span style="font-size:12pt">&nbsp;</span></p><p style=""><span style="color:#6d6d6d">&lt;/div&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;/body&gt;</span></p><p style=""><span style="color:#6d6d6d">&lt;/html&gt; </span></p></div>

--------

* 文字页面 [p-***.xhtml] ※例如「p-002.xhtml」

  与封面相同，但没有 `epub:type ="cover"`

  统一图像大小基于各自作品

--------

<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;!DOCTYPE html&gt;</span></p><p><span style="color:#6d6d6d">&lt;html</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="http://www.w3.org/1999/xhtml"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:epub="http://www.idpf.org/2007/ops"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&lt;head&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta charset="UTF-8"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;title&gt;</span><span style="color:#0000ff">作品名</span><span style="color:#6d6d6d">&lt;/title&gt;</span></p><p><span style="color:#6d6d6d">&lt;link rel="stylesheet" type="text/css" href="../style/</span><span style="color:#fb0007">fixed-layout-jp.css</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta name="viewport" content="width=</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">, height=</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/head&gt;</span></p><p><span style="color:#6d6d6d">&lt;body&gt;</span></p><p><span style="color:#6d6d6d">&lt;div class="main"&gt;</span></p><p><span>&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;svg xmlns="http://www.w3.org/2000/svg" version="1.1"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:xlink="http://www.w3.org/1999/xlink"</span></p><p><span style="color:#6d6d6d">&nbsp; width="100%" height="100%" viewBox="0 0 </span><span style="color:#0000ff">848 1200</span><span style="color:#6d6d6d">"&gt;</span></p><p><span style="color:#6d6d6d">&lt;image width="</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">" height="</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">" xlink:href="../image/</span><span style="color:#fb0007">i-002.jpg</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/svg&gt;</span></p><p><span>&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;/div&gt;</span></p><p><span style="color:#6d6d6d">&lt;/body&gt;</span></p><p><span style="color:#6d6d6d">&lt;/html&gt; </span></p></div>

-------

<参考>

在文本中指定图像映射（可点击的图）时，请进行以下操作：

* 在 `<a>` 标签的 `xlink:href` 属性中插入目标链接的文件名
* `<rect>` 标签的 `x` 和 `y` 属性指定点击范围的起始位置（左上角）的坐标
* `<rect>` 标签的 `width` 和 `height` 属性指定点击范围的大小

-----

<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;!DOCTYPE html&gt;</span></p><p><span style="color:#6d6d6d">&lt;html</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="http://www.w3.org/1999/xhtml"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:epub="http://www.idpf.org/2007/ops"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&lt;head&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta charset="UTF-8"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;title&gt;</span><span style="color:#0000ff">作品名</span><span style="color:#6d6d6d">&lt;/title&gt;</span></p><p><span style="color:#6d6d6d">&lt;link rel="stylesheet" type="text/css" href="../style/</span><span style="color:#fb0007">fixed-layout-jp.css</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta name="viewport" content="width=</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">, height=</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/head&gt;</span></p><p><span style="color:#6d6d6d">&lt;body&gt;</span></p><p><span style="color:#6d6d6d">&lt;div class="main"&gt;</span></p><p><span style="color:#6d6d6d">&lt;svg xmlns="http://www.w3.org/2000/svg" version="1.1"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:xlink="http://www.w3.org/1999/xlink"</span></p><p><span style="color:#6d6d6d">&nbsp; width="100%" height="100%" viewBox="0 0 </span><span style="color:#0000ff">848 1200</span><span style="color:#6d6d6d">"&gt;</span></p><p><span style="color:#6d6d6d">&lt;image width="</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">" height="</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">" xlink:href="../image/</span><span style="color:#fb0007">i-001.jpg</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span>&lt;a xlink:href="p-002.xhtml" target="_top"&gt;&lt;rect fill-opacity="0.0" x="476" y="1000" width="300" height="60"/&gt;&lt;/a&gt;</span></p><p><span>&lt;a xlink:href="p-colophon.xhtml" target="_top"&gt;&lt;rect fill-opacity="0.0" x="476" y="1075" width="300" height="60"/&gt;&lt;/a&gt;</span></p><p><span style="color:#6d6d6d">&lt;/svg&gt;</span></p><p><span style="color:#6d6d6d">&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;/div&gt;</span></p><p><span style="color:#6d6d6d">&lt;/body&gt;</span></p><p><span style="color:#6d6d6d">&lt;/html&gt; </span></p></div>

-----



#### 关于默认的 CSS 文件

##### 样式表的组成

fixed-layout-jp.css		······	从 xhtml 文件中调用的文件

固定布局不使用其他样式，因此不必支持@import

##### CSS文件的使用规则

* 原则上不修改默认 CSS

  原则上，本指南在示例中提供的 CSS 文件不作修改。 此 CSS 文件未考虑需要复杂规范的布局。 更改 CSS 内容本身时要小心，如下所示：

  ​	改变 class 的名字

  ​	给 class 添加心的属性

  ​	移动 class 的位置以改变优先级

  ​	重命名与其他 class 相关联的 class

  ​	追加新的 class

  ​	追加出版商的样式设定

* 避免重复的 id

  原本 id 只要求对于每个页面（XHTML文件）是唯一的，但是考虑到由多个文件组成的 EPUB 数据的配置，它被假定为一个作品中的唯一值

##### 创建自己的 CSS 文件

作为基本规则，建议保存为 UTF-8（无BOM）编码格式，并始终在文件开头插入 `@charset "UTF-8";`。

-------

#### 片假名-英文

コミックスコンテンツ comic's content

コンテン content

リーディングシステム reading system (rs)

レイアウト layout

パッケージ package

ファイル file

アイテム item

タイトル title

メイン タイトル main title

サブタイトル sub title

シリーズ series

カバー cover

ナビゲーション navigation

ページ page

システム system

コード code

テンプレート template

デフォルト default