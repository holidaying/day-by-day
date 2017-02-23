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
