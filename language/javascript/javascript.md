###闭包
```javascript
function buildList(list) {
    var result = [];
    for (var i = 0; i < list.length; i++) {
        var item = 'item' + i;
        result.push( function() {console.log(item + ' ' + list[i]+''+i)} );
    }
    return result;
}

function testList() {
    var fnlist = buildList([1,2,3]);
    for (var j = 0; j < fnlist.length; j++) {
        fnlist[j]();
    }
}
```
输出

```javascript
item2 undefined 3
item2 undefined 3
item2 undefined 3
```
因为数组并没有下标为3的项,所以undefined
那么为什么是item2 和 3 呢
首先var i 作用域为在buildList函数内(根据作用域提升)
但输出为`item2`
可见`for`循环的确执行到` i = 2`时就跳出了
但是在闭包内`i` 运算到了3 因为` i `作用域为 `buildList`
每次循环都会+1,等于2时跳出，但最后仍会对 `i=2` +`1`即`3`
这是闭包的特性之一
```javascript
for (let i = 0; i < list.length; i++) {
	let item = 'item' + i;
	result.push( function() {console.log(item + ' ' + list[i]+''+i)} 	);
}
```
将var换成let，因为let是块级作用域，每次for循环中let是独立的，
输出
```javascript
item0 1 0
item1 2 1
item2 3 2
```

item同理