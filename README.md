#点点看法

> 2017季度总结

###1.字符串改成驼峰方式
```
String.prototype.camelCase=function(){
if (this === "") {
  return "";
}
else {
    var arr = this.trim().split(' ');
    for (var i = 0; i < arr.length; i++) {
    arr[i] = arr[i][0].toUpperCase() + arr[i].slice(1);
}
 return arr.join('');}
}
```
###2.有意思的算法（真假美猴王）
http://www.tuicool.com/articles/I3M7ZzN
###3.`Math.floor()`和 `~~` 的使用区别
```Math.floor(-4.5)=5;
   Math.floor(4.5)=4;
   
   ~~-4.5=-4;
   ~~4.5=-4;
   ```
   都是取整数，但是`~~`纯粹是取整数，不参与数学性质，Math.floor()有明确的数学意义，向下取整。负数的时候存在明显区别
### 4.查找存在属性的对象
```
 function whatIsInAName(collection, source) {
  // What's in a name?
  var arr = [];
  var keys=Object.keys(source);
  arr = collection.filter(function(value){
        for(var i=0;i<keys.length;i++)
          {
              if(!value.hasOwnProperty(keys[i]) || value[keys[i]]!=source[keys[i]])
                {
                  return false;
                }
          }
      return true;
  });
  return arr;
}
whatIsInAName([{ first: "Romeo", last: "Montague" }, { first: "Mercutio", last: null }, { first: "Tybalt", last: "Capulet" }], { last: "Capulet" });
```
### 5.es6 Generator 形式上，Generator 函数是一个普通函数，但是有两个特征。一是，function关键字与函数名之间有一个星号；二是，函数体内部使用yield语句，定义不同的内部状态（yield在英语里的意思就是“产出”）。
* 1.yield普通数值
```
function* Hello(){
 yield 1;
 yield 2;
}
var hello = Hello();
console.log(hello.next());  // { value:1, done:false }
console.log(hello.next());  // {  value:2, done:false }
console.log(hello.next());  // { value:undefined, done:true }
需要next.value才能把值打印出来。
```
* 2.yield函数
```
function delay(time, cb){
 setTimeout(function(){
   cb && cb()
 },time);
}
function cl(){
  yieldDelay.next();
}
function* YieldDelay(){
  yield delay(3200,cl); 
  console.log('3200ms done!');
  yield delay(4400,cl);
  console.log('4400ms done!');
  yield delay(5500,cl);
  console.log('5500ms done!');
}
var yieldDelay = YieldDelay();
yieldDelay.next();
next是直接执行函数
```
* 3.可以直接执行yield后面的函数
```
function* Hello(){
 yield console.log("111");
 yield console.log("222");
}
var hello = Hello();
console.log(hello.next());  // { value:1, done:false }
console.log(hello.next());  // {  value:2, done:false }
console.log(hello.next());  // { value:undefined, done:true }
```
### 6.数字转成字母和字母转成数字str.charCodeAt(pos)和String.fromCharCode(number)
```
function fearNotLetter(str) {
  for(var i=0;i<str.length-1;i++)
    {
      if(str.charCodeAt(i+1)-str.charCodeAt(i)==2)
        {
          return String.fromCharCode(str.charCodeAt(i)+1);
        }
    }
  return undefined;
}
fearNotLetter("abce")
```
### 7.Array.from() 方法从一个类似数组或可迭代对象创建一个新的数组实例。[查看地址](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)Array.from()，reduce()，array.indexOf()合并数组去掉重复的数子
```
function uniteUnique(arrx) {
  var args = Array.from(arguments);
  var arr = args.reduce(function(prev,cur,index,array){
    return prev.concat(cur);
  });
  return arr.filter(function(item,index,array){
    return array.indexOf(item) === index;
  });
}

uniteUnique([1, 3, 2], [5, 2, 1, 4], [2, 1]);
```
### 8.技高一筹的正则表达式,带回调函数
```
function convertHTML(str) {
  return str.replace(/[&<>"']/g, function($0) {
        return "&" + {"&":"amp", "<":"lt", ">":"gt", '"':"quot", "'":"apos"}[$0] + ";";
    });
}

convertHTML("Dolce & Gabbana");
```
### 9.代码需要严谨，例如重构函数
```
String.prototype.repeatify = String.prototype.repeatify || function(times) {
   var str = '';
 
   for (var i = 0; i < times; i++) {
      str += this;
   }
 
   return str;
};
```
用||来判断是否定义过。

### 10.原生的http请求方式
```
var xhr = null;
if (window.XMLHttpRequest){// code for all new browsers
	  xhr=new XMLHttpRequest();
}
else if (window.ActiveXObject){// code for IE5 and IE6
	  xhr=new ActiveXObject("Microsoft.XMLHTTP");
}
xhr.onreadystatechange = function(){
	
    var XMLHttpReq = xhr;
    if (XMLHttpReq.readyState == 4) {
        if (XMLHttpReq.status == 200) {
        }
    }
};
xhr.open("GET", ulr, true);
// xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
xhr.send();
}
```
### 11.vue router2.0去掉#。
```
html5模式
当开启 history选项时，就打开了html5模式。去掉了#号。
注意
启用 HTML5 history 模式。利用 history.pushState() 和 history.replaceState() 来管理浏览历史记录。
注意： 当使用 HTML5 history 模式时，服务器需要被正确配置 以防用户在直接访问链接时会遇到404页面。
history的选项如上所说，需要正确配置以防止直接访问时404错误。
什么意思呢？
比如/foo/bar，这个路径是由vue-router跳转到的，而不是真实存在的路径，所以当你直接访问时返回的是404，除非你是在express项目中运行，所有的路径都转向了index.html。
而直接部署静态页的方式，你需要在nginx中配置rewrite参数，重新跳转到index.html页面上。
Nginx
 rewrite ^(.+)$ /index.html last;
 ```
 ### 12关于JSON字符串
 > json字符串必须是键和键值组成，如果有数组，数组里面也必须是对象的键和键值。json字符串不能尾部带有多余的，。否则json编译不通过
