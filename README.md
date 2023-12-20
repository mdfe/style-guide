# 明道前端规范

## 规范的规范
说明一些基础事项，并作为其他规范的准则。

### 原则和目的
* 风格统一，所有代码应该看上去像出自同一人之手。
* 易于理解，代码应当能够自解释，并有足够的文档。
* 提高质量，提供最佳实践，避免常见和易犯的错误。

### 表示要求级别的关键字
类似 RFC 2119，文档中出现的要求级别的定义如下，Code Review 遵照此标准。文档中不应该出现其他表示要求的词汇。
* 必须：表示绝对要求这样做。
* 禁止：表示绝对不要求这样做。
* 应该：表示一般情况下应该这样做，但是在有正当和充分的理由时可以忽视这个要求。
* 不应该：表示一般情况下不应该这样做，但是在有正当和充分的理由时可以忽视这个要求。
* 可以：表示这只是个建议，是完全是可选的。你可以这样做，也可以不这样做。

### 规范的执行
* Code Review
    + 通过 github 提交记录进行
    + 每周轮流由两位前端组成员分模块负责 review 工作
    + 发现的问题要求下次 review 之前完全改正

* eslint 等工具
    要求工具审查通过才能提交到远程仓库

### 浏览器兼容性
* IE 系列：IE10 及以上
* Chrome 内核/Firefox/Safari：国内占比 1% 以上的版本
* 其他主流国产套壳浏览器的 Chrome 内核模式
* 静态页面（尤其是首页和注册页面）：IE8 及以上

### 多语言规范
* _l()方法中禁止嵌套_l()方法
* 文案尽量不要断词，中间有变量的用%0、%1依次追加上去

## JavaScript 代码规范
适用 Web 前端的 JavaScript 代码规范。在进行 Web 前端 JavaScript 编码时应该遵守此规范。

### 语言规范

#### 代码格式
1. 文件中缩进必须统一。新文件应该使用 2 空格缩进，禁止使用 tab 符号。老代码应该遵循原来的缩进
2. 语句都必须有分号结尾，除了for, function, if, switch, try, while

    > 某些情况下如果不注意，漏掉分号可能会产生意料之外的结果

    ```js
    // bad
    MyClass.prototype.myMethod = function() {
      return 42;
    }
    (function() {
      // 一些代码
    })();
    
    var x = { 'i': 1, 'j': 2 }
    [normalVersion, ffVersion][isIE]();
    
    var THINGS_TO_EAT = [apples, oysters, sprayOnCheese]
    -1 == resultOfOperation() || die();
    ```
3. 代码块和方法的左大括号应该放在上一行行末，而不是另起一行

    ```js
    // bad
    function CSharpStyle() 
    {
    }
    ```
    ```js
    // good
    function JSStyle() {
    }
    ```
4. 如果通过 if 和 else 使用多行代码块，应该把 else 放在 if 代码块关闭括号的同一行。try/catch 同理

    ```js
    // bad
    if(a > b) {
      // 一些代码
    }
    else
    if(a < b) {
      // 另一些代码
    }
    ```
    ```js
    // good
    if(a > b) {
      // 一些代码
    } else if (a < b) {
      // 另一些代码
    }
    ```
5. 所有的循环体和判断体必须使用大括号括起来，即使只有一行

    > 如果不注意可能会导致代码与想法不符，并可能导致空悬 else 问题
6. 每行不应该超过 120 个字符

    > 便于在不左右滚动屏幕的情况下快速阅读代码
7. 运算符前后、左大括号前、逗号后应该有一个空格。行尾不应该有空格
8. 在对象和数组的声明中，逗号应该放在成员后而不是下一行。如果所有成员写在同一行，最后一个成员后不应该加逗号；否则最后一个成员后应该添加逗号

    > 最后一个成员添加逗号可以减少合并冲突

    ```js
    //good
    var obj = {a: 1, b: 2};
    var obj = {
      a: 1,
      b: 2,
    };
    ```
9. 长方法调用折行时，应该将 . 放在下一行。进行链式调用时，可以使用一定的缩进表示调用的对象和层级

    ```js
    //good
    $('body').hide()
      .append('div')
      .find('img')
        .remove()
        .end()
      .show();
    ```
10. 比较长的标识符或者数值, 不应该为了让代码好看些而手工对齐

    ```js
    //bad
    var a             = 1;
    var aLongVariable = 2;
    ```
    ```js
    //good
    var a = 1;
    var aLongVariable = 2;
    ```
11. 应该使用空行来划分一组逻辑上相关联的代码片段

#### 变量声明
1. 声明变量必须加上 var 关键字
2. 变量名必须含义明确，不应该使用单字母或难以理解的变量名。含义十分明确的情况下，短循环中可以使用实体首字母命名变量。应该避免错误的单词拼写，对已有的单词拼写错误在可控的情况下应该进行纠正
3. 普通（非模块）变量名、对象的属性名、非构造函数的方法名必须使用小驼峰(camelCase)命名法

     ```
     var variable;
     var obj = {a: 1};
     function someFunc() {}
     ```
4. 类和构造函数必须使用大驼峰(PascalCase)命名法；React 组件应该使用大驼峰命名法；模块名可以使用大驼峰命名法

    ```
    function Constructor(){}
    var inst = new Constructor();
    ```
5. 常量/枚举名必须使用全大写，单词间以下划线分隔

    ```
    var CHAT_SERVER = '';
    ```
6. 不应该暴露私有变量。外除 lodash 库和用来保存 this 引用的 _this 外，变量和属性名禁止以下划线开头
7. 保存 this 的引用时，变量名应该使用 this 所指代对象的有含义的名字。如果实在很难表达，可以使用 _this、self 或 that 

    ```js
    //not so good
    posts.forEach(function() {
      var _this = this;
      //...
    });
    ```
    ```js
    //good
    posts.forEach(function() {
      var post = this;
      //...
    });
    ```
8. 应该使用 var 声明每一个变量，并放在单独的行中

    > 减少合并冲突

    ```js
    //bad
    var a = 1,
        b = 2;
    ```
    ```js
    //good
    var a = 1;
    var b = 2;
    ```
9. 应该在作用域顶部声明变量
10. 可以给函数命名
11. 不应该重新定义同名变量

#### 类型
##### 基本类型
1. 应该使用原始值，不应该包装基本类型

    ```js
    //bad
    var box = new String('原始值');
    ```

##### 对象
1. 应该使用字面值创建对象

    ```js
    //bad
    var obj = new Object();
    ```
    ```js
    //good
    var obj = {};
    ```
2. 禁止使用保留字作为键，应该使用同义词(而不是同音词)替换

    ```js
    //bad
    var obj = {class: 'post'};
    var obj = {klass: 'post'};
    ```
    ```js
    //good
    var obj = {type: 'post'};
    ```
3. 应该使用 . 访问对象的属性，除非是通过变量，或键名中有特殊字符

    ```js
    //bad
    var a = obj['a'];
    ```
    ```js
    //good
    var a = obj.a;
    var a = obj[a];
    var b = obj['member b'];
    ```

##### 数组
1. 应该使用字面值创建数组

    ```js
    //bad
    var arr = new Array();
    ```
    ```js
    //good
    var arr = [];
    ```
2. 应该使用 push 方法向数组添加元素，而不是直接赋值

    ```js
    //bad
    arr[arr.length] = 1;
    ```
    ```js
    //good
    arr.push(1);
    ```
3. 应该使用 slice 方法进行数组拷贝，在 ES6 中应该使用 ...

    ```js
    //good
    var clone = arr.slice();
    //good(ES6)
    var clone = [...arr];
    ```
3. 应该使用 slice 方法将类数组对象(如 arguments)转换为数组

##### 字符串
1. 应该使用单引号表示字符串，除非字符串里有单引号

    ```js
    //bad
    var str = "How are you";
    ```
    ```js
    //good
    var str = 'How are you';
    var str = "I'm fine";
    ```
2. 长字符串可以使用 + 号连接并进行换行

    > &plus; 号连接字符串可读性比数组合并或 += 更高，并且在现代浏览器中性能更优
3. 对于 HTML 模版，应该使用模版引擎或 ES6 模版字符串进行渲染，而不是拼接字符串。3 行以下包括变量、10 行以下不包含变量的 html 拼接不要求使用模版引擎。
4. 应该使用 doT 模板引擎，并使用默认语法(使用默认的 `{{` 和 `}}`，流程控制应该尽可能使用模板引擎自带的语法而不是 JS 语句)
5. 如果一定要拼接 HTML 字符串，应该注意对变量进行 HTML 实体转码

    ```js
    //bad
    var html = '<div>' + htmlEncode(data.content) + '</div>';
    //bad
    var html = doT.template('<div><%= it.content%></div>')(data);
    ```
    ```js
    //not so good
    var html = `<div>${htmlEncode(data.content)}</div>`;
    //good
    var html = doT.template('<div>{{! it.content}}</div>')(data);
    ```

##### 函数
1. 禁止将函数声明放在非函数代码块(if、while 等)中，而是应该将其赋给一个变量

    ```js
    //bad
    if(a > 0) {
      function someFunc() {}
      someFunc();
    }
    ```
    ```js
    //good
    if(a > 0) {
      var someFunc = function someFunc() {}
      someFunc();
    }
    ```
2. 禁止将参数命名为 arguments
3. 形参过长时，可以使用单个对象传递参数。此时应该为每个参数添加详尽的注释
4. 函数返回多个值时，应该使用对象而不是数组

    ```js
    //bad
    function multiReturnValue() {
      return [1, 2];
    }
    ```
    ```js
    //good
    function multiReturnValue() {
      return {a: 1, b: 2};
    }
    ```
5. 可以使用函数声明代替函数表达式

    > 抛出异常时可以比较容易追踪到方法名

    ```js
    // ok
    var someFunc = function() {};
    //good
    function someFunc() {}
    ```
6. 函数可以返回 this 来方便链式调用。jQuery 组件应该返回 this
7. 使用闭包时应该注意避免产生循环引用

    ```js
    //bad
    function foo(element, a, b) {
      element.onclick = function() { /* uses a and b */ };
    }
    ```
    ```js
    //good
    function foo(element, a, b) {
      element.onclick = bar(a, b);
    }
    function bar(a, b) {
      return function() { /* uses a and b */ }
    }
    ```

#### 构造函数
1. 可以自定义一个 toString 方法。自定义的 toString 方法不应该有副作用或抛出异常
2. 在 ES6 中应该使用 class 代替构造函数。应该使用 extends 关键字进行继承

#### 比较和运算符
1. 应该使用 === 和 !==，避免使用 == 和 !=，除非是老代码/接口不确定类型
2. 应该了解不同类型的布尔类型转换方式，在 if 和三元运算符中使用较短的表达方式
3. 应该避免不必要的判断代码
4. 禁止在判断语句中进行赋值操作。应该避免 yoda 表达

    ```js
    //bad
    if (a = 1) {}
    if (1 === a) {}
    if (a === 0) {}
    function noA() {
      if(a) {
        return true;
      } else {
        return false;
      }
    }
    ```
    ```js
    //good
    if (a === 1) {}
    if (!a) {}
    function noA() {
      return !!a;
    }
    ```
4. 不应该使用 ~ 运算符进行 indexOf 的结果判断

    > 不够直观
    
    ```js
    //bad
    if(~list.indexOf(item)) {}
    ```
    ```js
    //good
    if(list.indexOf(item) !== -1) {}
    if(list.indexOf(item) >= 0) {}
    ```

#### 原型和工具方法
1. 禁止对内置对象进行原型修改
2. 应该避免使用老代码中顶级对象的原型扩展方法，使用工具方法代替
3. 应该优先使用工具库(lodash,jQuery)中的方法，缺少相关方法时再自行实现

    ```js
    //bad
    String.prototype.trim = function(str) {...}
    str = str.trim();
    ```
    ```js
    //good
    str = _.trim(str);
    str = $.trim(str);
    ```
4. 工具类和公共方法应该放在公共文件中。修改公共文件后必须告知全员

#### 严格模式
1. 应该遵守严格模式，即使没有使用 'use strict' 语句。可以使用 'use strict' 显式开启严格模式
2. 除底层工具库外，禁止使用 eval([string]), new Function([string]), setTimeout([string], …) 以及 setInterval([string], …) 等直接执行字符串的方式

#### 全局变量
1. 如无必要，应该避免引入 window/global 上的全局变量

#### 代码引用

    > 为启用 CSP 提供可能

1. 应该将 JavaScript 标签都放在外部文件中进行引用
2. 不应该内部引用 JavaScript
3. 禁止内联引用 JavaScript

    ```js
    //forbidden
    <img onclick="javascript:someFunc(this);">
    //bad
    <script>$(img).on('click', someFunc);</script>
    ```
    ```js
    //good
    <script src="bindEvents.js"></script>
    ```

#### 前后端数据交互
要求后端返回的数据遵守下列规范
1. 后端返回数据必须是 JSON 格式，并遵循变量命名规范
2. 如果数据表示特定的类型，则它必须是对应的类型而不是字符串

    ```js
    //bad
    {"allowDown": "ok","commentCount":"1"}
    ```
    ```js
    //good
    {"allowDown": true,"commentCount":1}
    ```
3. 除现有某些接口外，后端应该返回未编码过的数据，由前端进行编码。前端应该假设后端返回的数据都是不安全的

### jQuery
1. jQuery 对象的变量名应该使用 $ 开头
2. 应该缓存 jQuery 选择结果，或使用链式调用避免不必要的元素查询

    ```js
    //bad
    $('div').show();
    $('div').hide();
    ```
    ```js
    //good
    var $div = $('div');
    $div.show();
    $div.hide();
    //good
    $('div').show().hide();
    ```
3. 应该避免无用的选择。如果不需要用到父元素，应该使用单个选择器一次选中目标元素

    ```js
    //bad
    $('.parent #id').hide();
    ```
    ```js
    //good
    $('#id');
    //good
    var $parent = $('.parent');
    // do sth. with $parent
    $parent.find('#id').hide();
    ```
4. 如果需要在重复元素上绑定相同或类似的事件，应该使用事件委托，绑定在共同的父元素上

    ```js
    //bad
    $('ul li').on('click', function() {});
    ```
    ```js
    //good
    $('ul').on('click', 'li', function() {});
    ```
5. 绑定到 #container 或更上层元素(body、document、window 等)上的事件必须有表示对应模块的命名空间

    ```js
    //bad
    $('body').on('click', function() {});
    ```
    ```js
    //good
    $('body').on('click.feed', function() {});
    ```
6. 在事件中传递数据时，应该使用对象而不是原始值

    > 方便后期修改

    ```
    $(document).on('CUSTOM_EVENT', function(evt, arg) {});
    //good
    $(document).trigger('CUSTOM_EVENT', {a: 1})
    //bad
    $(document).trigger('CUSTOM_EVENT', 1)
    ```
7. 不应该直接拼接 ajax 请求参数，应该将其作为参数传给 jQuery。如果一定要手工拼接参数，需要注意使用 encodeURIComponent 进行转码

    ```js
    //forbidden
    $.get('ajaxpage.aspx?a=' + a);
    //bad
    $.get('ajaxpage.aspx?a=' + encodeURIComponent(a));
    ```
    ```js
    //good
    $.get('ajaxpage.aspx', {a: a});
    ```
8. 通过类名选择元素时应该添加有意义的钩子类，而不是样式类

    ```js
    //bad
    // <a class="ThemeColor3">动态</a>
    $('a.ThemeColor3').addClass('highlight');
    ```
    ```js
    //good
    // <a class="headLink ThemeColor3">动态</a>
    $('a.headLink').addClass('highlight');
    ```
9. 操作 dom 元素时，可以尽量批量修改、通过 display:none 隐藏元素后进行操作以减少重绘和重排列
10. 如无必要（如不存在兼容性问题且操作很简单），可以避免使用 jQuery

    > [You Might Not Need jQuery](http://youmightnotneedjquery.com/)

### ES 2016 (ES6)
1. const > let > var，应该尽量使用 const 和 let 代替 var；相同的声明方法应该放在一起
2. 声明对象中的属性和方法时应该使用简写，并将属性的简写放在前面

    ```js
    //bad
    var a = 1;
    var obj = {a: a, b: 2};
    var obj = {b: 2, a};
    ```
    ```js
    //good
    var a = 1;
    var obj = {a, b: 2};
    ```
3. 可以使用对象和数组的解构赋值

    ```js
    //good
    var {a, b} = obj;
    ```
4. 应该避免使用 arguments 对象，而是使用 ... 语法

    ```js
    //good
    function(...args) {
      args.forEach(arg => console.log(arg));
    }
    ```
5. 应该使用参数默认值，而非在方法中判断

    ```js
    //bad
    function(a, b) {
      b = typeof b === 'undefined' ? 1 : b;
    }
    ```
    ```js
    //good
    function(a , b = 1) {}
    ```
6. 使用参数默认值时应该避免副作用
7. 使用函数表达式时，应该尽量使用箭头函数，在方法体不长时应该省略大括号和 return

    ```js
    //good
    callback(obj => console.log(obj));
    ```

### JSX
待定

### 注释
1. 应该使用 jsdoc 格式进行注释，每个模块、方法声明、方法参数、公开变量、上都应该有注释。jQuery 参数暂时使用单行注释
2. 应该使用 // 进行单行注释
3. 应该使用 FIXME 表示问题，TODO 表示解决方案或代办事项

    ```js
    //good
    //FIXME: someFunc 未定义时会出异常
    someFunc();
    //TODO: 应该先判断 someFunc 是否定义
    someFunc();
    ```

### 参考
* [Airbnb JavaScript Style Guide](https://github.com/sivan/javascript-style-guide/)
* [Google JavaScript 编码规范指南](http://alloyteam.github.io/JX/doc/specification/google-javascript.xml)

## HTML 代码规范
### 语言规范
* 每个文件中的缩进必须统一。应该使用 4 空格缩进，老代码应该遵循原来的缩进
* 除 br、 hr、 img、 input、 link、 meta 外，其他标签必须闭合
* 属性应该使用双引号

    ```html
    //bad
    <a href='http://mingdao.com'></a>
    ```
    ```html
    //good
    <a href="http://mingdao.com"></a>
    ```
* 每个页面 html 结构必须完整，必须有 title 及合适的 meta 信息（列表待定）
* css link/style 标签应该写在页头，script 标签应该写在页尾

## CSS 代码规范
### 语言规范
* 每个文件中的缩进必须统一。应该使用 2 空格缩进，老代码应该遵循原来的缩进
* 类名应该使用小驼峰命名法则。如果使用 BEM 命名法，Block 可以使用大驼峰命名，Block 和 Element 之间使用 `-` 连接，Element 和 Modifier 之间使用 `--` 连接。禁止使用下划线

    ```css
    /* good */
    .mdDialog .confirmButton.disabled {}
    /* good */
    .MdDialog-confirmButton--disabled {}
    ```
* 类名应该含义明确，命名应该显示出语义而不是具体的呈现形式

    ```css
    /* bad */
    .red {
      color: red;
    }
    ```
    ```css
    /* good */
    .error {
      color: red;
    }
    ```
* 不应该使用 id 选择器，老代码可以不用修改

    > id 选择器优先级最高可能引起不必要的问题，并且不可重用
* 应该避免使用通用选择器 *
* 可以避免使用子选择器 >

    > 它的性能优于后代选择器，但会造成与 html 间的高耦合
* 选择器原则上不应该超过 4 级（Less 中嵌套不超过 3 层）
* 老代码不应该使用工具格式化代码。如果需要调整，手工调整
* 记住匹配规则是从右往左，避免将效率低的选择器写在右侧
* 规则声明的左大括号 { 后应该换行，前面应该加上一个空格
* 规则声明的右大括号 } 应该独占一行
* 分割选择器的逗号前不应该有空格，后面应该加上一个空格或换行

    ```css
    /* good */
    .shortNameA, .shortNameB {
      ...
    }
    /* good */
    .reallyReallyLongNameA,
    .reallyReallyLongNameB {
      ...
    }
    ```
* 每个属性必须写在单独的一行，冒号后面空一格

    ```css
    /* bad */
    body {font-size:12px;}
    ```
    ```css
    /* good */
    body {
      font-size: 12px;
    }
    ```
* 每个模块应该有顶级 class 作为命名空间

    ```css
    /* bad */
    .message{
      float:left;
    }
    ```
    ```css
    /* good */
    .mdAlertDialog .message{
      float:left;
    }
    ```
* 如非特殊需要，不应该使用行内样式和 style 标签，应该使用外联 css 文件
* 编写代码时必须使用无浏览器前缀的写法

    > 构建流程会自动加上合适的浏览器前缀
* 目前通用样式应该写入 basic.css(基础样式) 和 inStyle.css(登录后基础样式中)

### 模块化
待定

### 参考
* [Airbnb CSS Style Guide](https://github.com/Zhangjd/css-style-guide/)
* [编写高效的 CSS](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Writing_efficient_CSS)

## 图片相关优化
* 纯色图标应该优先使用 icon font
* 应该使用合适尺寸的图片并进行压缩，在质量和尺寸间合理取舍。禁止直接使用未压缩的原图或尺寸明显超过需要的图片
* 对于频繁出现的大量小图片，应该使用 CSS Sprite

## Git 提交规范
* 每个提交功能应该单一
* 提交信息必须可读、有明确含义并说明此次提交的内容。可以遵守一些规范的格式
* 禁止将临时调试代码提交到代码库，如一些不必要的 console.log

### 参考
* [Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)
