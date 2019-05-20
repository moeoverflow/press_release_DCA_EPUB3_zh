# 数字漫画协会 EPUB3 固定布局 规格指南 ver.1.0

デジタルコミック協議会 EPUB3 固定レイアウト 仕様ガイド ver.1.0 [原文 PDF](http://www.digital-comic.jp/press_release_DCA_EPUB3.pdf)

2012/11/22

--------

**— Work In Progress —**



本指南是用于漫画内容制作开发和阅读器（RS）的 EPUB3 固定布局规范。 目前，IDPF（[国际数字出版论坛](https://zh.wikipedia.org/w/index.php?title=國際數位出版論壇&action=edit&redlink=1) [International Digital Publishing Forum](http://idpf.org/)）指定的 EPUB3 规范中允许多样的表述，这导致了各方制作的文件有差别，因阅读器的差异不能顺利显示的情况。希望本指南的使用，能促进数字漫画的制作和出版，使尽可能更多的漫画在尽可能更多的电子书店上架，为读者带来丰富的阅读体验。

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

* root 文件夹的名字由出版社指定

* 文件和文件夹的名字原则上使用小写字母（META-INF 和（企业）管理代码等有个别规定除外）

* 根据元信息文件(opf)中的 `<item>` 标签，资源文件夹的名字应该为 item（规范允许任意名字）

  ```
  译注：opf文件是记录电子书元信息的文件，暂称“元信息文件(opf)”，下同
  ```

* 所有的资源文件应该放在 item 目录下的指定文件夹里：

  图片文件			：image 文件夹

  CSS 样式文件	：style 文件夹

  xhtml 文件		：xhtml 文件夹

* 以下文件的文件名不变

  root 目录下的 mimetype

  META-INF 目录下的 container.xml

  

## 2. 文件规范

* 正文文本每次换页时，都分割为新创建的xhtml文件

* 该文件的标题基于该作品的标题

  在 xhtml 文档中 `<title>` 标签的内容，除非出版商有特别规定的情况，都应该填上作品的标题，与元信息文件(opf)中的作品名一致。主副标题和系列名中的空格使用全角空格。合集等包含多个不同作品的情况，使用出版商指定的名字。

* 只在封面和导航文档中使用 epub:type

  在 EPUB 标准中，可以用 epub:type 的属性来指定页面的作用。但是，目前没有阅读器用到了这一特性，也无法保证使用这一特性的css文件的可用性 //TODO 。因此，目前仅指定未来阅读器采用可能性较高的两处。

  封面图片页面 `<body epub:type="cover" class="p-cover">`

  导航文档 `<nav epub:type="toc" id="toc">`
  
  epub:type属性应当写在class和id的前面 (?)  //TODO



## 3. 简单的编码规则

* 字符编码推荐 UTF-8N（无BOM）
* 换行符在同一个文件中不可混用（？）  //TODO
* 不推荐使用本指南中没有涉及到的 html 标签和 css 属性
* 若非因出版社的要求，不插入注释
* 正文中标签中属性的先后顺序是：`epub:type` → `class` → `id` → `src/href` → `alt`
* 为了避免混乱，`<p>` 标签尽可能不加 class 属性
* 正文 xhtml 文档中的 html 标签之后进行换行

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

除非另有说明，否则请使用以下模板和文件名规定。 如需要除此处列出的模板或文件名规定之外的模板或文件名规定的情况，请遵循各出版商的规定。

* 源（文本）的整理

关于源的格式，例如源中的换行符和缩进，以及元素中的标签属性顺序，按照出商的规定执行。 除非另有说明，否则请根据以下模板进行整理规范格式化。

* 关于模板中的颜色表示

<span style="color: #808080;">灰色</span>：所有作品共有的部分（原则上不更改）

<span style="color: #0005ff;">蓝色</span>：在所有作品共有的部分中，每个作品需要单独更改的部分

<span style="color: #ff0000;">红色</span>：使用此模板的作品特有的、应该注意的部分（原则上不更改）

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

* 如果阅读器具有显示 `<dc:title>` 信息的功能，所有内容一定会被阅读系统显示在屏幕上。

* 如果阅读器具有显示 `<dc:creator>` 信息的功能，并且可能有多个 `<dc:creator>` 的情况 ，所有内容一定会被阅读系统显示在屏幕的某处。（用于连接多个作者姓名的符号，和（各参与者）职责的表示，会由阅读器自行决定。）

* 是逐个划分多个作者姓名到多个 `<dc:creator>` ，还是将它们全部列在同一个 `<dc:creator>` 中，请遵循出版商的说明。 在分多个标签的情况下，应由出版商指定每个作者的“role”属性和显示顺序。

* 由 `file-as` 指定的排列用假名不会显示在读者的阅读器上。

* 文件ID（unique-identifier）的编码方案没有确定的制度，由出版商决定。没有特别规定的情况，可使用 uuid。

* 更新日期在没有特别规定的情况下，考虑到之后文件管理的便利，请使用预定交付的日期。

* 更新日期不会显示给读者。

* 封面图象的文件名在没有特别规定的情况下，为了阅读器显示缩略度的速度，请全部使用统一名称(cover.jpg)。

* 对于从左向右阅读的作品，`<spine>` 的 `page-progression-direction` 由 `rtl` 改为 `ltr`。

* 为了避免 `<spine>` 的 `<itemref>` 中 idref 属性重复的文件不被显示（如Readium），及页面死循环（如Firefox 的 EPUBReader），同一张图片多次出现的场合，以防万一建议准备一个单独的 xhtml 文件来调用图像（例如，white2.xhtml 为第二个白色图像）

* （本指南）与电书协的Reflow型EPUB3指南的不同之处有以下几点：

  ◇ `<package>` 标签增加 prefix 属性

  ◇ `<!-- Fixed-Layout Documents指定 -->` 部分增加两个 `<meta>` 标签

  ◇ 样式表只有 fixed-layout-jp.css

  ◇ 采用内置svg。SVG 直接嵌入 xhtml 文档中。考虑到一些不支持 svg 的阅读系统，在 `<item>` 的 xhtml 文件中的添加相应的图片作为备选

  ◇ 在封面页的 `<spine>` 中的 `<itemref>`标签内增加 `properties ="rendition: page-spread-center"`

示例代码

--------

<div style="font-size: 14px;"><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;package </span></p><p><span>&nbsp; </span><span style="color:#6d6d6d">xmlns="http://www.idpf.org/2007/opf"</span></p><p><span style="color:#6d6d6d">&nbsp; version="3.0"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&nbsp; unique-identifier="</span><span style="color:#0000ff">unique-id</span><span style="color:#6d6d6d">"</span></p><p><span style="color:#6d6d6d">&nbsp; </span><span style="color:#fb0007">prefix="rendition: http://www.idpf.org/vocab/rendition/#ebpaj: http://www.ebpaj.jp/"</span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&lt;metadata xmlns:dc="http://purl.org/dc/elements/1.1/"&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">作品名</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:title id="title"&gt;</span><span style="color:#0000ff">作品名</span><span style="color:#0000ff">1</span><span style="color:#6d6d6d">&lt;/dc:title&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#title" property="file-as"&gt;</span><span style="color:#0000ff">セイレツヨウサクヒンメイカナ</span><span style="color:#0000ff">01</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">著者名</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:creator id="</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">"&gt;</span><span style="color:#0000ff">著作者名</span><span style="color:#0000ff">1</span><span style="color:#6d6d6d">&lt;/dc:creator&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">" property="role" scheme="marc:relators"&gt;</span><span style="color:#0000ff">aut</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">" property="file-as"&gt; </span><span style="color:#0000ff">セ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">レ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ツ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ヨ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ウ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">チ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ョ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">サ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ク</span><span style="color:#0000ff"> </span><span style="color:#0000ff">シ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ャ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">メ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">カ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ナ</span><span style="color:#0000ff"> 01</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator01</span><span style="color:#6d6d6d">" property="display-seq"&gt;</span><span style="color:#0000ff">1</span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;dc:creator id="</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">"&gt;</span><span style="color:#0000ff">著作者名</span><span style="color:#0000ff">2</span><span style="color:#6d6d6d">&lt;/dc:creator&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">" property="role" scheme="marc:relators"&gt;</span><span style="color:#0000ff">aut</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">" property="file-as"&gt; </span><span style="color:#0000ff">セ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">レ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ツ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ヨ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ウ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">チ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ョ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">サ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ク</span><span style="color:#0000ff"> </span><span style="color:#0000ff">シ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ャ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">メ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">イ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">カ</span><span style="color:#0000ff"> </span><span style="color:#0000ff">ナ</span><span style="color:#0000ff"> 02</span><span style="color:#6d6d6d">&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#</span><span style="color:#0000ff">creator02</span><span style="color:#6d6d6d">" property="display-seq"&gt;</span><span style="color:#0000ff">2</span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">出版社名</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:publisher id="publisher"&gt;</span><span style="color:#0000ff">出版社名</span><span style="color:#6d6d6d">&lt;/dc:publisher&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta refines="#publisher" property="file-as"&gt;</span><span style="color:#0000ff">セイレツヨウシュッハ</span><span style="color:#0000ff">゚ンシャメイカナ</span><span style="color:#0000ff"> </span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">言語</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:language&gt;ja&lt;/dc:language&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">ファイル</span><span style="color:#6d6d6d">id --&gt;</span></p><p><span style="color:#6d6d6d">&lt;dc:identifier id="</span><span style="color:#0000ff">unique-id</span><span style="color:#6d6d6d">"&gt;</span><span style="color:#0000ff">urn:uuid:860ddf31-55a4-449a-8cc9-3c1837657a15</span><span style="color:#6d6d6d">&lt;/dc:identifier&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- </span><span style="color:#6d6d6d">更新日</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="dcterms:modified"&gt;</span><span style="color:#0000ff">2012-01-01T00:00:00Z</span><span style="color:#6d6d6d">&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- Fixed-Layout Documents</span><span style="color:#6d6d6d">指定</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#fb0007">&lt;meta property="rendition:layout"&gt;pre-paginated&lt;/meta&gt;</span></p><p><span style="color:#fb0007">&lt;meta property="rendition:spread"&gt;landscape&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- etc. --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="ebpaj:guide-version"&gt;1.1&lt;/meta&gt; </span></p><p><span style="color:#6d6d6d">&lt;/metadata&gt;</span></p><p><span style="color:#6d6d6d">&lt;manifest&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- navigation --&gt; </span></p><p><span style="color:#6d6d6d">&lt;item media-type="application/xhtml+xml" id="</span><span style="color:#0000ff">toc</span><span style="color:#6d6d6d">" href="</span><span style="color:#0000ff">navigation-documents.xhtml</span><span style="color:#6d6d6d">" </span><span style="color:#fb0007">properties="nav"</span><span style="color:#6d6d6d">/&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- style --&gt;</span></p><p><span style="color:#6d6d6d">&lt;item media-type="text/css" id="</span><span style="color:#fb0007">fixed-layout-jp</span><span style="color:#6d6d6d">" href="style/</span><span style="color:#fb0007">fixed-layout-jp.css</span><span style="color:#6d6d6d">"/&gt; </span></p><p><span style="color:#6d6d6d">&lt;!-- image --&gt;</span></p><p><span style="color:#6d6d6d">&lt;item media-type="image/</span><span style="color:#0000ff">jpeg</span><span style="color:#6d6d6d">" id="cover" </span><span>href="image/cover.</span><span style="color:#0000ff">jpg</span><span>"</span><span style="color:#6d6d6d"> </span><span style="color:#fb0007">properties="cover-image"</span><span style="color:#6d6d6d">/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-white" href="image/i-white.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-001" href="image/i-001.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-002" href="image/i-002.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-003" href="image/i-003.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-004" href="image/i-004.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-005" href="image/i-005.jpg"/&gt;</span></p><p><span>&lt;item media-type="image/jpeg" id="i-colophon" href="image/i-colophon.jpg"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;!-- xhtml --&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-cover" </span><span>href="image/cover.jpg"</span><span> </span><span style="color:#fb0007">properties="svg" fallback="cover"</span><span>/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-white" href="xhtml/p-white.xhtml" properties="svg" fallback="i-white"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-001" href="xhtml/p-001.xhtml" properties="svg" fallback="i-001"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-002" href="xhtml/p-002.xhtml" properties="svg" fallback="i-002"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-003" href="xhtml/p-003.xhtml" properties="svg" fallback="i-003"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-004" href="xhtml/p-004.xhtml" properties="svg" fallback="i-004"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-005" href="xhtml/p-005.xhtml" properties="svg" fallback="i-005"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-colophon" href="xhtml/p-colophon.xhtml" properties="svg" fallback="i-colophon"/&gt;</span></p><p><span>&lt;item media-type="application/xhtml+xml" id="p-white2" href="xhtml/p-white2.xhtml" properties="svg" fallback="i-white"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/manifest&gt;</span></p><p><span style="color:#6d6d6d">&lt;spine page-progression-direction="</span><span style="color:#0000ff">rtl</span><span style="color:#6d6d6d">"&gt; </span></p><p><span>&lt;itemref linear="yes" idref="p-cover" properties="</span><span style="color:#fb0207">rendition:page-spread-center</span><span>"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-white" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-001" properties="page-spread-left"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-002" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-003" properties="page-spread-left"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-004" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-005" properties="page-spread-left"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-colophon" properties="page-spread-right"/&gt;</span></p><p><span>&lt;itemref linear="yes" idref="p-white2" properties="page-spread-left"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/spine&gt;</span></p><p><span style="color:#6d6d6d">&lt;/package&gt;</span></p></div>

---------



<参考信息>

为了使页面快速地适配并显示所有页面固定大小的图像，建议在描述 OPF 文件中的标准大小时进行如下描述：

* 为 `<package>`标签增加固定布局用的前缀
* 为 `<metadata>`增加页面图片的标准大小
* 页面中显示的图像的的长宽，请在下文中蓝色的部分中以px为单位统一记录

-------
<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;package</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="http://www.idpf.org/2007/opf"</span></p><p><span style="color:#6d6d6d">&nbsp; version="3.0"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&nbsp; unique-identifier="unique-id"</span></p><p><span style="color:#6d6d6d">&nbsp; prefix="rendition: http://www.idpf.org/vocab/rendition/# </span></p><p><span style="width:36pt; display:inline-block">&nbsp;</span><span style="color:#6d6d6d">&nbsp;&nbsp;&nbsp; ebpaj: http://www.ebpaj.jp/ </span></p><p><span style="color:#fb0007">&nbsp; </span><span style="width:29.5pt; display:inline-block">&nbsp;</span><span style="color:#fb0007">&nbsp;&nbsp;&nbsp; fixed-layout-jp: http://www.digital-comic.jp/</span><span style="font-size:13pt">" </span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;metadata xmlns:dc="http://purl.org/dc/elements/1.1/"&gt; </span></p><p><span>&nbsp;</span></p><p style="text-align:center; "><span style="color:#fb0007">(</span><span style="color:#fb0007">※</span><span style="color:#fb0007">中略</span><span style="color:#fb0007">) </span></p><p><span>&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;!-- Fixed-Layout Documents</span><span style="color:#6d6d6d">指定</span><span style="color:#6d6d6d"> --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="rendition:layout"&gt;pre-paginated&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="rendition:spread"&gt;landscape&lt;/meta&gt; </span></p><p><span>&nbsp;</span></p><p><span style="color:#fb0007">&lt;!-- </span><span style="color:#fb0007">基準サイス</span><span style="color:#fb0007">゙</span><span style="color:#fb0007"> --&gt;</span></p><p><span style="color:#fb0007">&lt;meta property="fixed-layout-jp:viewport"&gt;width=</span><span style="color:#0000ff">848</span><span style="color:#fb0007">, height=</span><span style="color:#0000ff">1200</span><span style="color:#fb0007">&lt;/meta&gt;</span></p><p><span style="color:#fb0007">&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;!-- etc. --&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta property="ebpaj:guide-version"&gt;1.1&lt;/meta&gt;</span></p><p><span style="color:#6d6d6d">&lt;/metadata&gt;</span></p><p><span>&nbsp;</span></p><p style="text-align:center; "><span style="color:#fb0007">(</span><span style="color:#fb0007">※</span><span style="color:#fb0007">後略</span><span style="color:#fb0007">) </span></p></div>

-------

#### 4-4: navigation-documents.xhtml

* 链接项和列表的层次结构根据作品内容而变化
* 除非出版商另有指示，请只写入封面、目录和版权页面的链接
* 本规范不支持在导航文档中包含非链接项目
* 导航目录的实现样式由阅读器决定
* 将导航文档作为正文目录使用的情况，可参考下文中正文页面的例子，进行样式表等的引入
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

* 正文页面 [p-***.xhtml] ※例如「p-002.xhtml」

  与封面相同，但没有 `epub:type ="cover"`

  作品内图片大小统一  //TODO

--------

<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;!DOCTYPE html&gt;</span></p><p><span style="color:#6d6d6d">&lt;html</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="http://www.w3.org/1999/xhtml"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:epub="http://www.idpf.org/2007/ops"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&lt;head&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta charset="UTF-8"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;title&gt;</span><span style="color:#0000ff">作品名</span><span style="color:#6d6d6d">&lt;/title&gt;</span></p><p><span style="color:#6d6d6d">&lt;link rel="stylesheet" type="text/css" href="../style/</span><span style="color:#fb0007">fixed-layout-jp.css</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta name="viewport" content="width=</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">, height=</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/head&gt;</span></p><p><span style="color:#6d6d6d">&lt;body&gt;</span></p><p><span style="color:#6d6d6d">&lt;div class="main"&gt;</span></p><p><span>&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;svg xmlns="http://www.w3.org/2000/svg" version="1.1"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:xlink="http://www.w3.org/1999/xlink"</span></p><p><span style="color:#6d6d6d">&nbsp; width="100%" height="100%" viewBox="0 0 </span><span style="color:#0000ff">848 1200</span><span style="color:#6d6d6d">"&gt;</span></p><p><span style="color:#6d6d6d">&lt;image width="</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">" height="</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">" xlink:href="../image/</span><span style="color:#fb0007">i-002.jpg</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/svg&gt;</span></p><p><span>&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;/div&gt;</span></p><p><span style="color:#6d6d6d">&lt;/body&gt;</span></p><p><span style="color:#6d6d6d">&lt;/html&gt; </span></p></div>

-------

<参考>

在文本中指定图像映射（可点击图片）时，请进行以下操作：

* 在 `<a>` 标签的 `xlink:href` 属性中输入目标链接的文件名
* `<rect>` 标签的 `x` 和 `y` 属性指定点击范围的起始位置（左上角）的坐标
* `<rect>` 标签的 `width` 和 `height` 属性指定点击范围的大小

-----

<div><p><span style="color:#6d6d6d">&lt;?xml version="1.0" encoding="UTF-8"?&gt;</span></p><p><span style="color:#6d6d6d">&lt;!DOCTYPE html&gt;</span></p><p><span style="color:#6d6d6d">&lt;html</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns="http://www.w3.org/1999/xhtml"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:epub="http://www.idpf.org/2007/ops"</span></p><p><span style="color:#6d6d6d">&nbsp; xml:lang="ja"</span></p><p><span style="color:#6d6d6d">&gt;</span></p><p><span style="color:#6d6d6d">&lt;head&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta charset="UTF-8"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;title&gt;</span><span style="color:#0000ff">作品名</span><span style="color:#6d6d6d">&lt;/title&gt;</span></p><p><span style="color:#6d6d6d">&lt;link rel="stylesheet" type="text/css" href="../style/</span><span style="color:#fb0007">fixed-layout-jp.css</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;meta name="viewport" content="width=</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">, height=</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span style="color:#6d6d6d">&lt;/head&gt;</span></p><p><span style="color:#6d6d6d">&lt;body&gt;</span></p><p><span style="color:#6d6d6d">&lt;div class="main"&gt;</span></p><p><span style="color:#6d6d6d">&lt;svg xmlns="http://www.w3.org/2000/svg" version="1.1"</span></p><p><span style="color:#6d6d6d">&nbsp; xmlns:xlink="http://www.w3.org/1999/xlink"</span></p><p><span style="color:#6d6d6d">&nbsp; width="100%" height="100%" viewBox="0 0 </span><span style="color:#0000ff">848 1200</span><span style="color:#6d6d6d">"&gt;</span></p><p><span style="color:#6d6d6d">&lt;image width="</span><span style="color:#0000ff">848</span><span style="color:#6d6d6d">" height="</span><span style="color:#0000ff">1200</span><span style="color:#6d6d6d">" xlink:href="../image/</span><span style="color:#fb0007">i-001.jpg</span><span style="color:#6d6d6d">"/&gt;</span></p><p><span>&lt;a xlink:href="p-002.xhtml" target="_top"&gt;&lt;rect fill-opacity="0.0" x="476" y="1000" width="300" height="60"/&gt;&lt;/a&gt;</span></p><p><span>&lt;a xlink:href="p-colophon.xhtml" target="_top"&gt;&lt;rect fill-opacity="0.0" x="476" y="1075" width="300" height="60"/&gt;&lt;/a&gt;</span></p><p><span style="color:#6d6d6d">&lt;/svg&gt;</span></p><p><span style="color:#6d6d6d">&nbsp;</span></p><p><span style="color:#6d6d6d">&lt;/div&gt;</span></p><p><span style="color:#6d6d6d">&lt;/body&gt;</span></p><p><span style="color:#6d6d6d">&lt;/html&gt; </span></p></div>

-----



#### 关于默认的 CSS 文件

##### 样式表的组成

fixed-layout-jp.css		······	从 xhtml 文件中调用的文件

固定样式不支持@import，请勿使用其他样式

##### CSS文件的使用规则

* 原则上不修改默认 CSS

  原则上，请不要修改本指南在示例中提供的 CSS 文件。 此 CSS 文件未考虑需要复杂规范的布局。 更改以下 CSS 内容时要小心：

  ​	改变 class 的名字

  ​	给 class 添加属性

  ​	移动 class 的位置以改变优先级

  ​	重命名与其他 class 相关联的 class

  ​	追加新的 class

  ​	追加出版商的样式设定

* 避免重复的 id

  原本 id 只要求对于每个页面（XHTML文件）是唯一的，但是考虑到由多个文件组成的 EPUB 数据的配置，请保证id在作品（所有文件）中的单一性

##### 创建自己的 CSS 文件

作为基本规则，建议保存为 UTF-8（无BOM）编码格式，并始终在文件开头插入 `@charset "UTF-8";`。

-------

#### 片假名-英文

コミックコンテンツ （电子）漫画书

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