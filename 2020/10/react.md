# react初学(官网)
React 将代码片段组合成复杂的UI界面  
代码片段=>组件  
react的组件很多
1.react.component的子类
自己做一个 React 组件类。一个组件接收一些参数，我们把这些参数叫做 props（“props” 是 “properties” 简写），然后通过 render 方法返回需要展示在屏幕上的视图的层次结构。  
**render 返回了一个 React 元素**
### 通过 Props 传递数据
在父组件里`<子组件 [属性名]={[属性值]}></子组件>`  
在子组件写`{this.props.[属性名]}`
### 给组件添加交互功能
首先，在子组件的`render()`方法的返回值的xxx标签里添加函数
like
```css
<button className="square" onClick={function() { alert('click'); }}>
```
*注意*:
为了少输入代码，同时为了避免 this 造成的困扰，我们在这里使用箭头函数 来进行事件处理.
```onClick={()=>alert('click')}```用这种方式向onClick这个**prop**传入一个*函数*。  
* * 
我们用**state**来实现所谓的"记忆功能  
可以通过在React组件的构造函数中设置```this.state```来初始化state.
```js
class Square extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: null,
    };
  }
  ```
   ``` {this.state.value}```
>在 JavaScript class 中，每次你定义其子类的构造函数时，都需要调用 super 方法。因此，在所有含有构造函数的的 React 组件中，构造函数必须以 super(props) 开头。

* 将标签中的this.props.[属性名]替换成this.state.[属性名]
* 将函数```onClick={()=>alert('click')}```替换成```onClick={()=>this.setState({value:'x'})}  
**当你遇到需要同时获取多个子组件数据，或者两个组件之间需要相互通讯的情况时，需要把子组件的 state 数据提升至其共同的父组件当中保存。之后父组件可以通过 props 将状态数据传递到子组件当中。这样应用当中所有组件的状态数据就能够更方便地同步共享了。**
# State & 生命周期
## 向 class 组件中添加局部的 state
把 render() 方法中的 this.props.date 替换成 this.state.date ：
```js
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
添加一个 class 构造函数，然后在该函数中为 this.state 赋初值：
```js
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```
通过以下方式将 props 传递到父类的构造函数中：
```js
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```
Class 组件应该始终使用 props 参数来调用父类的构造函数。