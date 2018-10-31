# lodash
对于`Typescript 2.0`以后的版本
你想引用`loadsh`库

如果你执行
```javascript
npm install --save lodash 
```
使用
```javascript
import _ from "lodash";
```
会出错 `Cannot find module 'lodash'.`

应该还要执行
```javascript
npm install --save-dev @types/lodash
```
即需要把`loadsh`添加到`devDependencies`中
这时候再

```javascript
import _ from "lodash";
```
就没有问题了，或者使用
```javascript
import * as _ from "lodash";
```

取决于你使用的`Typescript`版本


# rimraf
```javascript
rimraf node_modules
```


# socket.io
想要实现下列效果
```javascript
let socket = io.connect("http://host");
socket.on("*", function(){});
```
即，接受后台传来的所有消息
，对于`socket.io 1.3.7`
可以这样实现
```javascript
let onevent = socket.onevent;
socket.onevent = function (packet) {
    let args = packet.data || [];
    onevent.call (this, packet);    
    packet.data = ["*"].concat(args);
    onevent.call(this, packet);    
};
```

# sass
安装失败时可尝试
```javascript
npm i node-sass --sass_binary_site=https://npm.taobao.org/mirrors/node-sass/
```