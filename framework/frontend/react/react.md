### React [https://reactjs.org/docs/getting-started.html](https://reactjs.org/docs/getting-started.html)

# 深拷贝

1. _.cloneDeep()

2. jQuery.extend()

3. JSON.stringify()

2022以后可使用

```typescript
structuredClone(value)
```

structuredClone [https://developer.mozilla.org/zh-CN/docs/Web/API/structuredClone#%E8%AF%AD%E6%B3%95](https://developer.mozilla.org/zh-CN/docs/Web/API/structuredClone#%E8%AF%AD%E6%B3%95)

## 兼容旧浏览器 [https://github.com/ungap/structured-clone](https://github.com/ungap/structured-clone)

```typescript
function deepClone(obj, hash = new WeakMap()) {
  if (obj === null) return obj; // 如果是null或者undefined我就不进行拷贝操作
  if (obj instanceof Date) return new Date(obj);
  if (obj instanceof RegExp) return new RegExp(obj);
  // 可能是对象或者普通的值  如果是函数的话是不需要深拷贝
  if (typeof obj !== "object") return obj;
  // 是对象的话就要进行深拷贝
  if (hash.get(obj)) return hash.get(obj);
  let cloneObj = new obj.constructor();
  // 找到的是所属类原型上的constructor,而原型上的 constructor指向的是当前类本身
  hash.set(obj, cloneObj);
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      // 实现一个递归拷贝
      cloneObj[key] = deepClone(obj[key], hash);
    }
  }
  return cloneObj;
}
```