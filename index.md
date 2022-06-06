---
layout: default
---

<h2 id="toc">內容目錄</h2>

<div markdown="1">
### [HTML](#html)

- [HTML 語法](#html-syntax)
- [HTML5 Doctype](#html5-doctype)
- [語言屬性](#language-attribute)
- [IE 相容模式](#ie-compatibility-mode)
- [字元編碼](#character-encoding)
- [附上 CSS 和 JavaScript](#css-and-javascript-includes)
- [實用性優先於純粹性](#practicality-over-purity)
- [屬性順序](#attribute-order)
- [二元屬性](#boolean-attributes)
- [精簡標記使用](#reduce-markup)
- [編輯器偏好設定](#editor-preferences)
</div>

<div markdown="1">
### [CSS](#css)

- [CSS 語法](#css-syntax)
- [宣告順序](#declaration-order)
- [顏色](#colors)
- [邏輯屬性](#logical-properties)
- [避免使用 @import](#avoid-imports)
- [Media Query 放置方法](#media-query-placement)
- [單一宣告](#single-declarations)
- [捷徑語法標記](#shorthand-notation)
- [在預處理器使用巢狀結構](#nesting-in-preprocessors)
- [在預處理器使用運算子](#operators-in-preprocessors)
- [註解](#comments)
- [Class 名稱](#class-names)
- [選擇器](#selectors)
- [子代與後代選擇器](#child-and-descendant-selectors)
- [組織結構](#organization)
</div>

## 黃金原則

確實要求每個人，或自己，時時刻刻都一致認同規範。不管大還是小，有錯誤的地方請大聲說出來。想要對這份程式碼編寫指南進行新增或貢獻，請[在 Github 開 Issue](https://github.com/mdo/code-guide/issues/new)。

> 每行程式碼，不管有多少人參與，應該要看起來是一個人寫出來的。

## HTML

<div markdown="1">
### 語法
{: #html-syntax }

- 不以大寫使用標籤，包含 Doctype。
- 使用 2 個空白的 Soft Tab—這是可以保證程式碼在任何環境，都長得一樣的唯一方法。
- 巢狀裡面元素應該要縮排一次（2 個空白）。
- 屬性一定要用雙引號，絕不使用單引號。
- 在自帶關閉符號的元素不在尾端加上斜線－[HTML5 規格](https://html.spec.whatwg.org/multipage/syntax.html#syntax-start-tag)提到：這不是必需的。
- 不能省略非必要的關閉標籤（例如：`</li>` 或 `</body>`）。
</div>

```html
<!doctype html>
<html>
  <head>
    <title>頁面標題</title>
  </head>
  <body>
    <img src="images/company-logo.png" alt="Company">
    <h1 class="hello-world">Hello, world!</h1>
  </body>
</html>
```

<div markdown="1">
### HTML5 Doctype
{: #html5-doctype }

每一個 HTML 頁面的開頭，都要確實使用[標準模式](https://developer.mozilla.org/en-US/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)，就可以盡可能在每個瀏覽器的模樣是一致。為了跟語法建議一致，使用小寫。

</div>

```html
<!doctype html>
<html>
  <head>
    <!-- ... -->
  </head>
  <body>
    <!-- ... -->
  </body>
</html>
```

<div markdown="1">
### 語言屬性
{: #language-attribute }

根據 HTML5 規格：

> Authors are encouraged to specify a lang attribute on the root html element, giving the document's language. This aids speech synthesis tools to determine what pronunciations to use, translation tools to determine what rules to use, and so forth.

從[規格](https://html.spec.whatwg.org/multipage/semantics.html#the-html-element)，深入閱讀 `lang` 屬性。前往 <abbr title="Internet Assigned Numbers Authority">IANA</abbr> 查看[語言代碼清單](https://www.iana.org/assignments/language-subtag-registry/language-subtag-registry)。
</div>

```html
<html lang="en">
  <!-- ... -->
</html>
```

<div markdown="1">
### IE 相容模式
{: #ie-compatibility-mode }

現今，除非得要支援 IE10 或更舊版，已經不需要加上 Internet Explorer 文件的相容 `<meta>` 標籤。這組標籤已經在 IE11 棄用，Microsoft Edge不管是舊版或其它版本，也都不會用到。

詳細資訊請看這篇[很讚的 Stack Overflow 文章](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do)。
</div>

```html
<!-- 適用於 IE10 以前 -->
<meta http-equiv="x-ua-compatible" content="ie=edge">
```

<div markdown="1">
### 字元編碼
{: #character-encoding }

明確宣告字元編碼，就可以確保輸出的內容是正確的。這樣也可以使用一般文字，而不是 HTML Entity。例如：只要編碼與文件是相符的，就可以用 `—` 取代 `&emdash;`。有些 XML 的保留字元，像是與符號 (&)、不換行空格、少於/多於與引號，可能還是得要用 HTML 字元 Entity。

建議使用 UTF-8 編碼。
</div>

```html
<head>
  <meta charset="utf-8">
</head>
<body>
  <p>破折號就這樣使用—毋需得用上 HTML Entity。</p>
</body>
```

<div markdown="1">
### 附上 CSS 和 JavaScript
{: #css-and-javascript-includes }

根據 HTML5 的規格，附上 CSS 和 JavaScript 檔案 通常不需要指定 `type`，因為 `text/css` 和 `text/javascript` 已經是各自的預設值。

#### HTML5 規格連結

- [使用 link](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-link-element)
- [使用 style](https://www.w3.org/TR/2011/WD-html5-20110525/semantics.html#the-style-element)
- [使用 script](https://www.w3.org/TR/2011/WD-html5-20110525/scripting-1.html#the-script-element)
</div>

```html
<!-- 外部 CSS -->
<link rel="stylesheet" href="code-guide.css">

<!-- 文件內的 CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="code-guide.js"></script>
```

<div markdown="1">
### 實用性優先於純粹性
{: #practicality-over-purity }

應該要竭盡可能維護 HTML 的標準與情境，但不應犧牲實用性。只要有可能，盡量以最低的複雜度，使用最少的標記。
</div>

```html
<!-- 很好 -->
<button>...</button>

<!-- 不好 -->
<div class="btn" onClick="...">...</div>
```

<div markdown="1">
### 屬性順序
{: #attribute-order }

為了可以更容易閱讀程式碼，HTML 屬性應該要按照以下的順序列出。

- `class`
- `id`, `name`
- `data-*`
- `src`, `for`, `type`, `href`, `value`
- `title`, `alt`
- `role`, `aria-*`
- `tabindex`
- `style`

先放最常用來辨識元素的屬性－`class`、`id`、`name` 然後是 `data`。接下來是元素專用的其它屬性；最後是無障礙設計和樣式相關的屬性。
</div>

```html
<a class="..." id="..." data-toggle="modal" href="#">
  範例連結
</a>

<input class="form-control" type="text">

<img src="..." alt="...">
```

<div markdown="1">
### 二元屬性
{: #boolean-attributes }

二元屬性是不需要宣告值的屬性。XHTML 要求得宣告值，但 HTML 沒這樣需求。

想要深入理解，可以查閱 [WhatWG 這段，對二元屬性的意見](https://html.spec.whatwg.org/multipage/common-microsyntaxes.html#boolean-attributes)。

> 元素出現二元屬性，代表是 true 值，而沒有該屬性，就是 false 值。

如果屬性<strong>一定得要</strong>有值，雖然**不需要這樣做**，可以按照 WhatWG 的規範：

> 如果有設定屬性，它的值不是空白字串，就是 [...] 屬性的唯一名稱，且前方和尾端沒有空白。

簡單來說，就是**不要加上值**。
</div>

```html
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

<div markdown="1">
### 精簡標記使用
{: #reduce-markup }

撰寫 HTML 的時候，盡可能避免多餘的上層元素。很多時候，這得要不斷修改與重構，但會產生比較少 HTML。
</div>

```html
<!-- 不怎麼好 -->
<span class="avatar">
  <img src="...">
</span>

<!-- 好多了 -->
<img class="avatar" src="...">
```

<div markdown="1">
### 編輯器偏好設定
{: #editor-preferences }

為了避免常見的不一致程式碼，以及讓人覺得骯髒的差異比對，要把編輯器做以下設定：

- 使用設定為 2 個空白的 Soft Tab。
- 儲存時，移除尾端的空白字元。
- 編碼設定為 UTF-8。
- 在檔案的尾端新增一行。

請考慮把這些偏好設定在專案的 `.editorconfig` 檔案裡記錄、設定起來。實際案例請看 [Bootstrap](https://github.com/twbs/bootstrap/blob/main/.editorconfig) 做的。深入閱讀 [EditorConfig](https://editorconfig.org)。
</div>

## CSS

<div markdown="1">
### 語法
{: #css-syntax }

- 使用 2 個空白的 Soft Tab—這是可以保證程式碼在任何環境，都長得一樣的唯一方法。
- 為選擇器 ，每個選擇器都維持一行。
- 為了易讀性考量，宣告的起頭大括號前面，要有空格。
- 宣告的關閉大括號要換行。
- 每個宣告的 `:` 後面要有空白。
- 每個宣告應該都是單獨一行，錯誤回報才會更精準。
- 所有宣告的結尾都有分號。最後一個宣告可以省略，然而，沒有的話，程式碼更容易出錯。
- 以逗號分隔的屬性值，應該要在逗號之後加個空白（例如：`box-shadow`）。
- 以空白分隔的方式使用顏色屬性（例如：`color: rgb(0 0 0 / .5)`），[詳見顏色段落](#colors)。
- 屬性值或顏色參數不需要前綴 0（例如：`.5` 取代 `0.5`，以及 `-.5px` 取代 `-0.5px`）。
- 16 進位值全部是小寫，例如：`#fff`。小寫字母因為通常有比較多獨特的形狀，在掃視文件的時候，辨識容易許多。
- 盡可能使用捷徑來表示16 進位值，例如：`#fff` 取代 `#ffffff`。
- 選擇器裡的屬性值要用引號，例如：`input[type="text"]`。[只有一些特定情況才不必這樣做](https://mathiasbynens.be/notes/unquoted-attribute-values#css)，這是保持一致的好方法。
- 數值為 0 的時候，避免指定單位。例如：`margin: 0;`，而不是 `margin: 0px;`。

對於這裡的用語有問題？請看 Wikipedia 上，[階層式樣式表的語法段落](https://en.wikipedia.org/wiki/Cascading_Style_Sheets#Syntax)。
</div>

```scss
// 壞 CSS
.selector, .selector-secondary, .selector[type=text] {
  padding:15px;
  margin:0px 0px 15px;
  background-color:rgba(0, 0, 0, 0.5);
  box-shadow:0px 1px 2px #CCC,inset 0 1px 0 #FFFFFF
}

// 好 CSS
.selector,
.selector-secondary,
.selector[type="text"] {
  padding: 15px;
  margin-bottom: 15px;
  background-color: rgb(0 0 0 / .5);
  box-shadow: 0 1px 2px #ccc, inset 0 1px 0 #fff;
}
```

<div markdown="1">
### 宣告順序
{: #declaration-order }

屬性宣告應根據以下順序群組起來：

1. 設定位置
2. Box 模型
3. 文字排版
4. 視覺
5. 其它

因為位置設定，可以把元素從一般文件佈局流動移除，並且覆蓋 Box 模型，因此要放在最前面。接著是 Box 模型，不管是 Flex、Float、Grid 或 Table－因為掌控了元件的尺寸、擺放位置與靠齊。其它東西，因為是在元件的**裡面**發生，或者，不會影響前面兩段，而放在後面。

雖然 `border` 是 Box 模型的一部分，大多數的系統都一律把 [`box-sizing`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) 設定為 `border-box`，不讓 `border-width` 影響整體尺寸。加上讓 `border` 跟 `border-radius` 更靠近，這就是改放在視覺段落的原因。

預處理器的 Mixin 和函式要擺在最合適的地方。例如：`border-top-radius()` 這個 Mixin 要放在 `border-radius` 屬性的位置；而 `responsive-font-size()` 會在 `font-size` 屬性的位置。

在 [Bootstrap](https://getbootstrap.com) 使用的 [Stylelint 屬性順序](https://github.com/stormwarning/stylelint-config-recess-order)，可以看到所有屬性列表與其順序。
</div>

```scss
.declaration-order {
  // 設定位置
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 100;

  // Box 模型
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 100px;
  height: 100px;

  // 文字排版
  font: normal 14px "Helvetica Neue", sans-serif;
  line-height: 1.5;
  color: #333;
  text-align: center;
  text-decoration: underline;

  // 視覺
  background-color: #f5f5f5;
  border: 1px solid #e5e5e5;
  border-radius: 3px;

  // 其它
  opacity: 1;
}
```

<div markdown="1">
### 邏輯屬性
{: #logical-properties }

邏輯屬性，是以 *block* 和 *inline* 等抽象名詞替代方向與尺寸屬性。block 預設代表垂直方向（上與下），而 inline 是水平方向（右與左）。在所有現代與持續發展的瀏覽器，都可以開始在 CSS 使用這些值。

**為什麼要使用邏輯屬性？**不是每個語言都跟英文一樣，是從左往右看。因此，[Writing Mode](https://developer.mozilla.org/en-US/docs/Web/CSS/writing-mode) 得能靈活使用。有了邏輯屬性，就可以輕鬆地支援水平或垂直書寫的與言（像是中文、日文與韓文）。另外，通常寫起來比較簡短、簡易。

**延伸閱讀**

- [CSS Logical Properties and Values – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Logical_Properties)
- [CSS Logical Properties and Values — CSS Tricks](https://css-tricks.com/css-logical-properties-and-values/)
- [CSS Writing Modes – MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Writing_Modes)
</div>

```scss
// 未使用邏輯屬性
.element {
  margin-right: auto;
  margin-left: auto;
  border-top: 1px solid #eee;
  border-bottom: 1px solid #eee;
}

// 使用邏輯屬性
.element {
  margin-inline: auto;
  border-block: 1px solid #eee;
}
```

<div markdown="1">
### 顏色
{: #colors }

所有主流瀏覽器都已支援 [CSS Color Levels 4](https://www.w3.org/TR/css-color-4/)，`rgba()` 和 `hsla()` 現在跟 `rgb()` 和 `hsl()` 是相同的，也就是說，能夠在 `rgb()` 和 `hsl()` 修改 Alpha 值。同時，顏色值也支援以空白分隔的新語法。為了能跟未來的 CSS 顏色函式相容，就用新語法吧。

除了顏色值和語法，挑選顏色的時候也要確保符合 [WCAG 的最小對比度](https://webaim.org/articles/contrast/)（16px 以下是 4.5:1；以上是3:1）。

**延伸閱讀：**

- [Smashing Magazine - A Guide To Modern CSS Colors](https://www.smashingmagazine.com/2021/11/guide-modern-css-colors/)
- [`rgb()` - MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/color_value/rgb)
</div>

```css
.element {
  color: rgb(255 255 255 / .65);
  background-color: rgb(0 0 0 / .95);
}
```

<div markdown="1">
### 避免使用 `@import`
{: #avoid-imports }

跟 `<link>` 相比，`@import` 比較慢，增加額外的頁面請求，也可能會導致其它無法預知的問題。要避免使用，可以採用以下替代方案：

- 使用多個 `<link>` 元素
- 以預處理器 [Sass](https://sass-lang.com/) 或 [Less](https://lesscss.org/) 把 CSS 編譯為單一檔案
- 使用 Rails、Jekyll 和其它環境提供的串接 CSS 檔案功能

[閱讀 Steve Souders 的文章](https://www.stevesouders.com/blog/2009/04/09/dont-use-import/)了解更多細節。
</div>

```html
<!-- 使用 link 元素 -->
<link rel="stylesheet" href="core.css">

<!-- 避免使用 @import -->
<style>
  @import url("more.css");
</style>
```

<div markdown="1">
### Media Query 放置方法
{: #media-query-placement }

把要用到的 Media Query，盡可能放在相關的規則附近。不要打包成另一組獨立的樣式表，或是文件的尾端。這樣做，之後會讓其他人不小心就錯過。請參考常見的設置方法。
</div>

```css
.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (min-width: 480px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

<div markdown="1">
### 單一宣告
{: #single-declarations }

假設有組規則只有**一個宣告**，為了可讀性和更方便編輯，請考慮拿掉換行。其它有多重宣告的規則，還是要分成多行。

這樣做的主因是偵測錯誤－例如：CSS 驗證工具指出在 183 行的語法錯誤。在單一宣告的情境，就直接看到。而多重宣告的情況，為了整齊，還是得要多行。
</div>

```scss
// 用一行來表示單一宣告
.span1 { width: 60px; }
.span2 { width: 140px; }
.span3 { width: 220px; }

// 多重宣告則是每個一行
.sprite {
  display: inline-block;
  width: 16px;
  height: 15px;
  background-image: url("../img/sprite.png");
}
.icon           { background-position: 0 0; }
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
```

<div markdown="1">
### 捷徑語法標記
{: #shorthand-notation }

只有在必需強調想設定所有可用的值時，才會使用捷徑宣告。常見濫用的捷徑屬性包含：

- `padding`
- `margin`
- `font`
- `background`
- `border`
- `border-radius`

通常，沒有必要設定捷徑屬性所提供的全部值。舉例來說：HTML 的標題只設定了上和下的 margin，因此，有必要的時候，僅需要覆蓋這兩個值。`0` 值代表覆蓋了瀏覽器預設值，或先前指定的值。

過度使用捷徑屬性，會導致沒必要的覆蓋和預料之外的副作用，讓程式碼更雜亂。

Mozilla Developer Network 有一篇針對[捷徑屬性](https://developer.mozilla.org/en-US/docs/Web/CSS/Shorthand_properties)的優良文章，寫給不熟標記和行為的人。
</div>

```scss
// 不良範例
.element {
  margin: 0 0 10px;
  background: red;
  background: url("image.jpg");
  border-radius: 3px 3px 0 0;
}

// 優良範例
.element {
  margin-bottom: 10px;
  background-color: red;
  background-image: url("image.jpg");
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
}
```

<div markdown="1">
### 在預處理器使用巢狀結構
{: #nesting-in-preprocessors }

使用預處理器也要避免不必要的巢狀結構－保持簡單，避免反向巢狀結構。只有在得要把樣式根據上一層設定範圍時，或是有多個元素，才做成巢狀。

**延伸閱讀：**

- <a href="https://markdotto.com/2015/07/20/css-nesting/">Nesting in Sass and Less</a>
</div>

```scss
// 沒有巢狀結構
.table > thead > tr > th { … }
.table > thead > tr > td { … }

// 有巢狀結構
.table > thead > tr {
  > th { … }
  > td { … }
}
```

<div markdown="1">
### 在預處理器使用運算子
{: #operators-in-preprocessors }

所有數學運算都用括號包起來，值、變數與運算子之間都有一個空白，可讀性就會大幅改善。
</div>

```scss
// 不良範例
.element {
  margin: 10px 0 @variable*2 10px;
}

// 優良範例
.element {
  margin: 10px 0 (@variable * 2) 10px;
}
```

<div markdown="1">
### 註解
{: #comments }

程式碼是由人所撰寫和維護。確保程式碼對其他人來說，是充分描述的、有良好註解，以及友善的。好的程式碼註解傳達情境或目標。請勿僅僅重複描述元件或 Class 名稱。在預處理器撰寫 CSS 時，使用 `//` 語法。發布到正式環境時，要移除所有註解。

比較龐大的註解記得要寫成完整的句子；一般記錄使用簡潔的詞彙。
</div>

```scss
// 不良範例
// 彈出視窗的標題
.modal-header {
  ...
}

// 優良範例
// 包覆 .modal-title 和 .modal-close 的元素
.modal-header {
  ...
}
```

<div markdown="1">
### Class 名稱
{: #class-names }

- Class 要保持小寫，並且使用半型橫槓（而不是底線或 camelCase）。半型橫槓在相關的 Class 就像天然的分隔（例如：`.btn` 和 `.btn-danger`）。
- 避免過度和隨意的捷徑標記。**按鈕**取為 `.btn` 很有用，但 `.s` 就沒有意義了。
- Class 要盡量保持簡短與簡潔。
- 使用有意義的名稱；使用結構或有意義的名稱，而不是根據外表。
- 根據最近的上層或基礎 Class 來取前綴詞。
- 使用 Class 名稱 `.js-*` 來標注行為（而不是樣式）。但是，這些 Class 不會出現在 CSS 檔案裡。

在編寫 Custom Properties 和預處理器變數名稱時，使用這些規則也很好用。
</div>

```scss
// 不良範例
.t { ... }
.red { ... }
.header { ... }

// 優良範例
.tweet { ... }
.important { ... }
.tweet-header { ... }
```

<div markdown="1">
### 選擇器
{: #selectors }

- Use classes over generic element tags for more explicit and reliable styling that isn't dependent on your markup.
- Avoid using several attribute selectors (e.g., `[class^="..."]`) on commonly occuring components. Browser performance is known to be impacted by these.
- Keep selectors short and strive to limit the number of elements in each selector to three.
- Scope classes to the closest parent `only` when necessary (e.g., when not using prefixed classes).

**延伸閱讀：**

- [Scope CSS classes with prefixes](https://markdotto.com/2012/02/16/scope-css-classes-with-prefixes/)
- [Stop the cascade](https://markdotto.com/2012/03/02/stop-the-cascade/)
</div>

```scss
// 不良範例
span { ... }
.page-container #stream .stream-item .tweet .tweet-header .username { ... }
.avatar { ... }

// 優良範例
.avatar { ... }
.tweet-header .username { ... }
.tweet .avatar { ... }
```

<div markdown="1">
### 子代與後代選擇器
{: #child-and-descendant-selectors }

When necessary, it may be helpful to use [the child combinator (`>`)](https://developer.mozilla.org/en-US/docs/Web/CSS/Child_combinator) to limit the cascade of some styles in elements like `<table>`s that are often recursively nested. Use it to limit styles to the immediate children elements of a parent element to avoid unnecessary overrides later on.
</div>

```css
.custom-table > tbody > tr > td,
.custom-table > tbody > tr > th {
  /* ... */
}
```

<div markdown="1">
### 組織結構
{: #organization }

- Organize sections of code by component.
- Develop a consistent commenting hierarchy.
- Use consistent white space to your advantage when separating sections of code for scanning larger documents.
- When using multiple CSS files, break them down by component instead of page. Pages can be rearranged and components moved.
</div>

```scss
//
// Component section heading
//

.element { ... }


//
// Component section heading
//
// Sometimes you need to include optional context for the entire component. Do that up here if it's important enough.
//

.element { ... }

// Contextual sub-component or modifer
.element-heading { ... }
```
