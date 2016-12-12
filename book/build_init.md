# mocha 打造 API 測試環境

打造測試的第一步，通常都會從環境建立起，而很多人都會卡在這個環節就開始不知道該如何進行。

跟著這邊一步一步進行吧。

## 安裝

 * [node.js](http://nodejs.org/)

這個是一定要安裝的

## 執行程式

```
npm i -g mocha@2.5.3
```

因為接下來會採用 babel 設定 es2015, `await` 等語言特性，所以建立大家都可以先以這個版本為主。

## 設定測試

```
mkdir test_project && cd test_project // test_project 可以為任何名字
mkdir test
touch mocha.opts
npm init
npm i supertest chai babel-core babel-polyfill --save
```

## 修改檔案

`test/mocha.opts`

```
-t 500000
--require chai
--reporter dot
```

## 第一次後端測試檔案

`test/apiTest.spec.js`

```

(function() {

  var request = require('supertest');
  var request = request('http://localhost:3000');
  
  require('chai').should();
  require("babel-core/register");
  require("babel-polyfill");

  before(function(done) {
    done();
  });

  after(function(done) {
    return setTimeout(() => {
      done()  
    }, 2000);
  });

}());

```

可以透過以下指令進行基本測試會得到

```
mocha test/apiTest.spec.js
```


回傳內容如下，

```
Generating report files...



  Test topic here
    ✓ detail describe


  1 passing (3s)
```

上述到底用了哪些東西，我們下回分享。




