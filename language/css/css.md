# 处理空隙

对于`inline-block`引发的间隙

在其父元素添加
```css
    font-size: 0;
    letter-spacing: -3px;
```

# 固宽布局取960px

960可分为这些等宽的列，其他数值则没有
1  2  3  4  5  6  8  10  12  15  16  20  24  30  32  40  48  60  64  80  96  120  160  192  240  320  480  960

# FLEX children set heigth 100%

```css
    .container {
    height: 20em;
    display: flex;
    flex-direction: column;
    border: 5px solid black
    }
    .item {
    flex: 1;
    border-bottom: 1px solid white;
    }
    .item-inner {
    height: 100%;
    width: 100%;
    display: table;
    }
    a {
    background: orange;
    display: table-cell;
    vertical-align: middle;
    }
```

```html
<div class="container">
  <div class="item">
    <div class="item-inner">
      <a>Button</a>
    </div>
  </div>

  <div class="item">
    <div class="item-inner">
      <a>Button</a>
    </div>
  </div>

  <div class="item">
    <div class="item-inner">
      <a>Button</a>
    </div>
  </div>
</div>
```

won't work for chrome 70+ version but fit for 80+ version

try

```css
    .item {
        height: 100%;
        width: 100%;
        display: flex;
    }
```

or

```css
    .item {
        flex-grow: 1;
        flex-basis: 0;
        border-bottom: 1px solid white;
    }
```
