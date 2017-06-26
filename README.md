# HTMLMinifier

[![NPM version](https://img.shields.io/npm/v/html-minifier.svg)](https://www.npmjs.com/package/html-minifier)
[![Build Status](https://img.shields.io/travis/kangax/html-minifier.svg)](https://travis-ci.org/kangax/html-minifier)
[![Dependency Status](https://img.shields.io/david/kangax/html-minifier.svg)](https://david-dm.org/kangax/html-minifier)
[![devDependency Status](https://img.shields.io/david/dev/kangax/html-minifier.svg)](https://david-dm.org/kangax/html-minifier?type=dev)
[![Gitter](https://img.shields.io/gitter/room/kangax/html-minifier.svg)](https://gitter.im/kangax/html-minifier)

[HTMLMinifier](http://kangax.github.io/html-minifier/) 是一个高度 **可配置**, **经过良好测试**, 基于javascript的HTML压缩器。

关于它是 [如何工作](http://perfectionkills.com/experimenting-with-html-minifier/#how_it_works), [每个选项的描述](http://perfectionkills.com/experimenting-with-html-minifier/#options), [测试结果](http://perfectionkills.com/experimenting-with-html-minifier/#field_testing) 和 [结论](http://perfectionkills.com/experimenting-with-html-minifier/#cost_and_benefits) 等各种细节，请查看 [相关的博客](http://perfectionkills.com/experimenting-with-html-minifier/) 。

[在线获取测试套件](http://kangax.github.io/html-minifier/tests/).

也可以查看 [Ruby版](https://github.com/stereobooster/html_minifier), 以及 Node.js版, [Grunt插件](https://github.com/gruntjs/grunt-contrib-htmlmin), [Gulp 模块](https://github.com/jonschlinkert/gulp-htmlmin), [koa中间件版](https://github.com/koajs/html-minifier) and [Express 中间件版](https://github.com/melonmanchan/express-minify-html).

关于类似于 lint 的功能，可以看看 [HTMLLint](https://github.com/kangax/html-lint).

## 缩小化工具比较

How does HTMLMinifier compare to other solutions — [HTML Minifier from Will Peavy](http://www.willpeavy.com/minifier/) (1st result in [Google search for "html minifier"](https://www.google.com/#q=html+minifier)) as well as [htmlcompressor.com](http://htmlcompressor.com) and [minimize](https://github.com/Swaagie/minimize)?

| Site                                                                        | Original size *(KB)* | HTMLMinifier | minimize | Will Peavy | htmlcompressor.com |
| --------------------------------------------------------------------------- |:--------------------:| ------------:| --------:| ----------:| ------------------:|
| [Google](https://www.google.com/)                                           | 46                   | **43**       | 46       | 48         | 46                 |
| [HTMLMinifier](https://github.com/kangax/html-minifier)                     | 129                  | **100**      | 108      | 113        | 108                |
| [CNN](http://www.cnn.com/)                                                  | 134                  | **123**      | 131      | 132        | 127                |
| [Amazon](http://www.amazon.co.uk/)                                          | 200                  | **168**      | 192      | 195        | n/a                |
| [Stack Overflow](http://stackoverflow.com/)                                 | 220                  | **170**      | 178      | 186        | 176                |
| [BBC](http://www.bbc.co.uk/)                                                | 228                  | **188**      | 221      | 228        | 216                |
| [New York Times](http://www.nytimes.com/)                                   | 235                  | **158**      | 181      | 178        | 165                |
| [Bootstrap CSS](http://getbootstrap.com/css/)                               | 272                  | **260**      | 269      | 229        | 269                |
| [Wikipedia](https://en.wikipedia.org/wiki/President_of_the_United_States)   | 550                  | **502**      | 530      | 548        | 529                |
| [NBC](http://www.nbc.com/)                                                  | 649                  | **617**      | 646      | 649        | n/a                |
| [Eloquent Javascript](http://eloquentjavascript.net/1st_edition/print.html) | 870                  | **815**      | 840      | 864        | n/a                |
| [ES6 table](http://kangax.github.io/compat-table/es6/)                      | 4105                 | **3467**     | 3871     | n/a        | n/a                |
| [ES6 draft](https://tc39.github.io/ecma262/)                                | 5512                 | **4919**     | 5066     | n/a        | n/a                |

## 可选项快速参考

默认情况下，大部选项都是禁用的。

| 可选项                         | 描述     | 默认值 |
|--------------------------------|-----------------|---------|
| `caseSensitive`                | 以大小写敏感的方式处理属性 (用于自定义 HTML 标签) | `false` |
| `collapseBooleanAttributes`    | [忽略布尔值属性的属性值](http://perfectionkills.com/experimenting-with-html-minifier/#collapse_boolean_attributes) | `false` |
| `collapseInlineTagWhitespace`  | 当压缩元素时，不要在内联元素 `display:inline;` 间留下空格。必须与 `collapseWhitespace=true` 结合使用 | `false` |
| `collapseWhitespace`           | [ 在文档树中压缩文本节点的空格 ](http://perfectionkills.com/experimenting-with-html-minifier/#collapse_whitespace) | `false` |
| `conservativeCollapse`         | 总是压缩至一个空白字符 (永远不要完全删除). 必须同 `collapseWhitespace=true` 结合使用 | `false` |
| `customAttrAssign`             | 允许支持自定义属性分配表达式的正则表达式数组 (例如. `'<div flex?="{{mode != cover}}"></div>'`) | `[ ]` |
| `customAttrCollapse`           | Regex that specifies custom attribute to strip newlines from (e.g. `/ng-class/`) | |
| `customAttrSurround`           | Arrays of regex'es that allow to support custom attribute surround expressions (e.g. `<input {{#if value}}checked="checked"{{/if}}>`) | `[ ]` |
| `customEventAttributes`        | 允许为 `minifyJS` 提供定制事件属性的正则表达式数组。 (e.g. `ng-click`) | `[ /^on[a-z]{3,}$/ ]` |
| `decodeEntities`               | 尽可能使用直接的Unicode字符 | `false` |
| `html5`                        | 根据 HTML5 规范解析输入的内容 | `true` |
| `ignoreCustomComments`         | 当匹配正则表达式数组时，允许忽略某些注释 | `[ /^!/ ]` |
| `ignoreCustomFragments`        | 当匹配正则表达式数组时，允许忽略某些片段 (e.g. `<?php ... ?>`, `{{ ... }}`, etc.)  | `[ /<%[\s\S]*?%>/, /<\?[\s\S]*?\?>/ ]` |
| `includeAutoGeneratedTags`     | Insert tags generated by HTML parser | `true` |
| `keepClosingSlash`             | 在单标签元素上保留尾部的斜杠 | `false` |
| `maxLineLength`                | 指定最大行长度。 压缩输出的内容将在有效的html分割点上换行。 |
| `minifyCSS`                    | 最小化 style 元素和 style 属性中的CSS (使用 [clean-css](https://github.com/jakubpawlowicz/clean-css)) | `false` (could be `true`, `Object`, `Function(text)`) |
| `minifyJS`                     | 最小化 script 元素和事件属性中的javascript (使用 [UglifyJS](https://github.com/mishoo/UglifyJS2)) | `false` (could be `true`, `Object`, `Function(text, inline)`) |
| `minifyURLs`                   | 最小化各种属性中的URL (使用 [relateurl](https://github.com/stevenvachon/relateurl)) | `false` (could be `String`, `Object`, `Function(text)`) |
| `preserveLineBreaks`           | 当标签之间的换行有空白时，永远压缩成一行(永远不完全删除)。必须结合 `collapseWhitespace=true` 一起使用 | `false` |
| `preventAttributesEscaping`    | 防止属性值的转义 | `false` |
| `processConditionalComments`   | Process contents of conditional comments through minifier | `false` |
| `processScripts`               | Array of strings corresponding to types of script elements to process through minifier (e.g. `text/ng-template`, `text/x-handlebars-template`, etc.) | `[ ]` |
| `quoteCharacter`               | 用于属性值的引号 (' 或 ") | |
| `removeAttributeQuotes`        | [在可能的情况下，删除属性值的引号](http://perfectionkills.com/experimenting-with-html-minifier/#remove_attribute_quotes) | `false` |
| `removeComments`               | [去除 HTML 注释](http://perfectionkills.com/experimenting-with-html-minifier/#remove_comments) | `false` |
| `removeEmptyAttributes`        | [删除所有空白值的属性](http://perfectionkills.com/experimenting-with-html-minifier/#remove_empty_or_blank_attributes) | `false` (could be `true`, `Function(attrName, tag)`) |
| `removeEmptyElements`          | [删除所有空内容的元素](http://perfectionkills.com/experimenting-with-html-minifier/#remove_empty_elements) | `false` |
| `removeOptionalTags`           | [删除可选的标签](http://perfectionkills.com/experimenting-with-html-minifier/#remove_optional_tags) | `false` |
| `removeRedundantAttributes`    | [删除值为默认值的属性](http://perfectionkills.com/experimenting-with-html-minifier/#remove_redundant_attributes) | `false` |
| `removeScriptTypeAttributes`   | 删除 `script` 标签的 `type="text/javascript"`. `type` 属性为其它值时保持不变 | `false` |
| `removeStyleLinkTypeAttributes`| 删除 `style` 和 `link` 标签的 `type="text/css"`. `type` 属性为其它值时保持不变 | `false` |
| `removeTagWhitespace`          | 尽可能在属性之间移除空格。 **注意：这可能导致无效的HTML** | `false` |
| `sortAttributes`               | [根据频率对属性进行排序](#sorting-attributes--style-classes) | `false` |
| `sortClassName`                | [根据频率对样式类进行排序](#sorting-attributes--style-classes) | `false` |
| `trimCustomFragments`          | 修剪 `ignoreCustomFragments` 周围的空白. | `false` |
| `useShortDoctype`              | [用短的 `doctype` (HTML5) 替换 `doctype` ](http://perfectionkills.com/experimenting-with-html-minifier/#use_short_doctype) | `false` |

### 对属性/样式类排序

Minifier options like `sortAttributes` and `sortClassName` won't impact the plain-text size of the output. However, they form long repetitive chains of characters that should improve compression ratio of gzip used in HTTP compression.

## 特殊情况

### 忽略大块标记

If you have chunks of markup you would like preserved, you can wrap them `<!-- htmlmin:ignore -->`.

### 保留 SVG 标签

SVG tags are automatically recognized, and when they are minified, both case-sensitivity and closing-slashes are preserved, regardless of the minification settings used for the rest of the file.

### 操作无效的标记

HTMLMinifier **不能操作无效的或部分的标记**. 这是因为它将标记解析为树结构,  然后修改它 (删除指定删除的内容, 忽略指定忽略的内容, etc.), 然后从该树结构中创建并返回标记。

输入标记 (e.g. `<p id="">foo`)

↓

标记以一种树的形式的内部表示 (e.g. `{ tag: "p", attr: "id", children: ["foo"] }`)

↓

转换的内部表示 (e.g. removal of `id` attribute)

↓

输出结果标记 (e.g. `<p>foo</p>`)

HTMLMinifier can't know that original markup was only half of the tree; it does its best to try to parse it as a full tree and it loses information about tree being malformed or partial in the beginning. As a result, it can't create a partial/malformed tree at the time of the output.

## 安装使用说明

From NPM for use as a command line app:

```shell
npm install html-minifier -g
```

From NPM for programmatic use:

```shell
npm install html-minifier
```

From Git:

```shell
git clone git://github.com/kangax/html-minifier.git
cd html-minifier
npm link .
```

## 用法

For command line usage please see `html-minifier --help`

### Node.js

```js
var minify = require('html-minifier').minify;
var result = minify('<p title="blah" id="moo">foo</p>', {
  removeAttributeQuotes: true
});
result; // '<p title=blah id=moo>foo</p>'
```

## 运行基准的测试

Benchmarks for minified HTML:

```shell
node benchmark.js
```
