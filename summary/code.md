### 表格驱动法
---
情况1
```javascript
if(a === 1) do
if(a === 2) do
```
这样写
```javascript
const arr = [...props]
for(const i in arr){
    if(a === arr[i]) do
}
```

情况2
```javascript
if(a === 1) return 'a1'
if(a === 2) return 'a2' 
```
这样写

```javascript
const obj = {
    1:'a1',
    2:'a2'
}

function getStr(type){
    return obj[type];
}
```


---
### 分支预测
---
当代码需要判断时,如下
```javascript
for(const i in arr ){
    if(arr[i] > 5){}
}
```
对于下列两个数组他们的处理速度不一样
```javascript
const sort = [1,3,4,5,6,7,8]

const random = [6,1,8,5,3,7,4]
```
处理a的速度是要大于b的
因为CPU有个处理机制叫`分支预测`

>`分支预测`简单的说就是当要做判断时,如果是第一次判断,CPU会随机预测一个分支来进行(预先写要做的分支的指令)
>如果预测是正确的,那么就执行预先写的指令,
>如果不是,那么预先写的指令就百写了,会滚回到分支开始重新判断
>这会消耗性能,如果数据量大的话,会很严重
>如果不是第一次,就根据之前的预测结果判断下一次的分支走向

例如 预测了 a > 5 但是错误,下一次就会预测 a <= 5

CPU先预测了了 <=5的分支,预测结果
对于数组sort
```javascript
TTTFTTT
```
对于数组random
```javascript
FTFFTFT
```

>那么显而易见,如果预测结果一直是正确的,那么CPU不用回退指令,也就避免了`分支惩罚`
>所以处理一个`已排序`的数组速度是要快上不少的

#####避免分支惩罚



---
###同步和异步
---