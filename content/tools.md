## 工具

### HTML-to-Mithril 模板转换器

如果您已经有了 HTML 写的网页，并且希望将它转换成一个 Mithril 的模板，可以使用下面的工具进行手动转换。

[模板转换器](http://arthurclemens.github.io/mithril-template-converter/index.html)

### 自动 HTML-to-Mithril 模板转换器

现有名为 [MSX](https://github.com/insin/msx) 的由 Jonathan Buchanan 开发的工具，允许您使用 HTML 的语法编写模板，然后在每次文件更改时把它们自动编译成 JavaScript。

此工具对拥有编写风格不同、功能关注点迥异的成员的团队来说相当有用。对于喜欢使用 HTML 语法来维护模板的人来说也是如此。

该工具允许您编写像这样的代码：

```javascript
todo.view = function() {
	return <html>
		<body>
			<input onchange={m.withAttr("value", app.vm.description)} value={app.vm.description()}/>
			<button onclick={app.vm.add}>Add</button>
		</body>
	</html>
};
```

注意，因为上面的代码并不是合法的 JavaScript，所以这种语法只能被预处理编译工具使用。此工具现已提供为一个[Gulp.js](http://gulpjs.com) 脚本。

此工具也可使用 [Rails gem 获得](https://github.com/mrsweaters/mithril-rails)，此 gem 包由 Jordan Humphreys 创建。

### Mithril 模板编译器

您可以预编译 Mithril 模板使其运行得更快。更多信息请参见这个页面:

[编译模板](optimizing-performance.md#compiling-templates)

### Typescript 支持

<!-- tnl: 原文作 Typescript，故此处不大写。 -->
现有一个类型定义文件，可以让 Mithril 支持 Typescript。

[mithril.d.ts](http://mithril.js.org/mithril.d.ts)

您可以通过添加一个指向 Typescript 文件的引用来使用它。这将允许编译器对 Mithril API 的调用进行类型检查。

```javascript
/// <reference path="mithril.d.ts" />
```

### IE 浏览器的兼容性

Mithril 依赖于一些 ECMAScript 5 的特性，即：`Array::indexOf`、`Array::map` 和 `Object::keys`，以及 `JSON` 对象。IE8 缺乏对这些特性的原生支持。

为 IE8 添加这些特性支持，最简单的方法是使用这个脚本：

```html
<script src="https://cdnjs.cloudflare.com/ajax/libs/es5-shim/4.0.3/es5-shim.min.js"></script>
```

这将为浏览器提供所需的所有新特性。另外，你也可以选择性地让浏览器支持某个特性：

```html
<script src="http://cdn.polyfill.io/v1/polyfill.min.js?features=Array.prototype.indexOf,Object.keys,Function.prototype.bind,Array.prototype.forEach,JSON"></script>
```
您还可以使用其他方式以便让 IE7 支持这些特性。

-	[ES5 Shim](https://github.com/es-shims/es5-shim) 或 Mozilla.org 的 [Array::indexOf](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/indexOf), [Array::map](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) 和 [Object::keys](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)

-	[JSON2.js](https://github.com/douglascrockford/JSON-js/blob/master/json2.js)

Mithril 也依赖于 XMLHttpRequest。如果您希望支持 IE6，您需要 [a shim for it](https://gist.github.com/Contra/2709462)。 IE7 及以下版本不支持跨域 AJAX 请求。

此外，请注意 `m.route` 模式依赖 `history.pushState`，此 API 可以实现从一个页面跳转到另一个页面，而不刷新浏览器。[IE9 及以下版本浏览器](http://caniuse.com/#search=pushstate) 不支持此功能，实现时将会优雅地使用页面刷新来替代。


翻译：@justjavac，更新 (2016/6/20)：@ttnl