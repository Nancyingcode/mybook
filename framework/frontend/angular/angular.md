  ### Angular [https://angular.cn/guide/quickstart](https://angular.cn/guide/quickstart)

  # Angular6+的兼容

  使用@angular/element出错
  修改tsconfig.json 将输入版本改为`es2015`或`ES6` 默认为 `ES5`
  ```javascript
  "module": "es2015",
  ```

  # Input()

  对于带 Input() 注解的变量, 在 constructor无法获取到他，会返回 `null`
  通过`ngOnInit`获取它的值


  # 打包优化

- 减少打包体积

  ```javascript
  ng build --prod --aot --output-path=prod --base-href ./
  ```