### lodash
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

### rimraf
```javascript
rimraf node_modules
```