# wg-office
一次前端笔试题
2017季度总结

1.字符串改成驼峰方式

<code>
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

</code>

2.有意思的算法（真假美猴王）
http://www.tuicool.com/articles/I3M7ZzN
