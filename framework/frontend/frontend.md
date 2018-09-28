
###`constructor`与 `componentDidMount`
在react中
`constructor`在每次函数实例化后执行，是一个默认方法，用来初始化属性(依赖注入)
这样使用
```javascript
constructor(props) {
	super(props);
	this.state = {date: new Date()};
}
```
`componentDidMount`在页面dom渲染完成后调用，用来处理函数的调用
这样使用
```javascript
componentDidMount() {
		this.timer = setInterval(function () {
    }.bind(this), 100);
}
```
`componentDidMount`与`Angular`中的`ngOnInit`类似
`ngOnInit`在组件即DOM创建后调用