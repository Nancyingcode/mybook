  ### Angular [https://angular.cn/guide/quickstart](https://angular.cn/guide/quickstart)

  # Angular6+的兼容

  使用@angular/element出错
  修改tsconfig.json 将输入版本改为`es2015`或`ES6` 默认为 `ES5`
  ```json
  {"module": "es2015"},
  ```

  # Input()

  对于带 Input() 注解的变量, 在 constructor无法获取到他，会返回 `null`
  通过`ngOnInit`获取它的值


  # 打包优化

  减少打包体积

  ```shell
  ng build --prod --aot --output-path=prod --base-href ./
  ```

  # 组件交互
  官方文档 [https://angular.cn/guide/component-interaction](https://angular.cn/guide/component-interaction)
  
  # 服务端渲染注意事项

  1. 对于引用，避免 通过`src/app`来引入，再打服务包时会出错

  # Server Side Rending

  ##　处理浏览器API

  1. `document` `navigator` 等

  通过自己注入模块实现,例如 `domino` npm包
  
  server.ts代码示例
  ```javascript
  // These are important and needed before anything else
  // tslint:disable-next-line:no-import-side-effect
  import 'reflect-metadata';
  // tslint:disable-next-line:no-import-side-effect
  import 'zone.js/dist/zone-node';

  import { enableProdMode } from '@angular/core';
  import { renderModuleFactory } from '@angular/platform-server';

  import * as express from 'express';
  import { readdirSync, readFileSync } from 'fs';
  import { join } from 'path';

  // Faster server renders w/ Prod mode (dev mode never needed)
  enableProdMode();

  // Express server
  const app = express();

  const PORT = process.env.PORT || 4000;
  const DIST_FOLDER = join(process.cwd(), 'dist');

  const FROENT_FOLDER = 'client';
  const SERVER_FOLDER = 'server';

  // Our index.html we'll use as our template
  const template = readFileSync(join(DIST_FOLDER, FROENT_FOLDER, 'index.html')).toString();

  const domino = require('domino');
  const win = domino.createWindow(template);

  // tslint:disable-next-line:no-string-literal
  global['window'] = win;
  Object.defineProperty(win.document.body.style, 'transform', {
    value: () => {
      return {
        enumerable: true,
        configurable: true
      };
    }
  });

  // tslint:disable-next-line:no-string-literal
  global['document'] = win.document;

  // tslint:disable-next-line:no-string-literal
  global['CSS'] = null;


  // global.navigator.userAgent = global.navigator.userAgent || 'all';

  // * NOTE :: leave this as require() since this file is built Dynamically from webpack
  const { AppServerModuleNgFactory, LAZY_MODULE_MAP } = require(`./dist/${SERVER_FOLDER}/main`);

  const { provideModuleMap } = require('@nguniversal/module-map-ngfactory-loader');

  app.engine('html', (_, options, callback) => {
    renderModuleFactory(AppServerModuleNgFactory, {

      // Our index.html
      document: template,
      url: options.req.url,
     
      // DI so that we can get lazy-loading to work differently (since we need it to just instantly render it)
      extraProviders: [
        provideModuleMap(LAZY_MODULE_MAP)
      ]
    }).then(html => {
      callback(null, html);
    });
  });

  app.set('view engine', 'html');
  app.set('views', join(DIST_FOLDER, FROENT_FOLDER));

  // Server static files from /browser
  app.get('*.*', express.static(join(DIST_FOLDER, FROENT_FOLDER)));

  // All regular routes use the Universal engine
  app.get('*', (req, res) => {
    res.render(join(DIST_FOLDER, FROENT_FOLDER, 'index.html'), { req });
  });

  // Start up the Node server
  app.listen(PORT, () => {
    console.log(`Node server listening on http://localhost:${PORT}`);
  });
  ```

  2. 页面存储

  需要判断是服务端环境还是浏览器环境

  `angular/core` 提供了 `PLATFORM_ID` 代表运行环境
  `angular/common` 提供了 `isPlatformBrowser`　来判断环境，需要 `PLATFORM_ID`

  代码示例
  ```typescript
  import { isPlatformBrowser } from '@angular/common';
  import { Inject, OnInit, PLATFORM_ID } from '@angular/core';

  @Component({
    selector: 'app-root',
    template: ``,
    styles: [``]
  })

  export class AppComponent implements OnInit {

    constructor(@Inject(PLATFORM_ID) private platformId: any) {}

    ngOnInit(): void {
      if(isPlatformBrowser(this.platformId)) {
        // do storage here
      }
    }
  }
  ```