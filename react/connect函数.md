## 关于react-redux中的connect函数
### 示例代码
```bash
'use strict';
import React from 'react';

import {
    connect
} from 'react-redux';
class demo extends React.Component {
    constructor(props) {
        super(props);
        this.state = {

        }

    }

    render() {

        return (
            <div className="page-content">

            </div>
          )
    }
}
export default connect(state => {
    return {
        demo: state.demo
    }
})(demo);
```
### 作用
 连接React组件与 Redux store ，允许我们将 store 中的数据作为 props 绑定到组件上。
### 使用

```bash
const App = () => {
  return (
    <Provider store={store}>
      <demo/>
    </Provider>
  )
};
```
* Provider 内的任何一个组件（比如这里的 demo），如果需要使用 state 中的数据，就必须是「被 connect 过的」组件——使用 connect 方法对「你编写的组件（MyComp）」进行包装后的产物

```bash
export default connect(state => {
    return {
        demo: state.demo
    }
})(demo);
```
* connect 函数可以将redux的小状态机单独传入react组件（即只传入你需要的部分），不必把state全部传入，如上面示例中就只传入了state.demo.
* 当readux里面相应的值改变时，connect会重新调用，生成新的props，这样react组件接受新的props,就会重新渲染。
### 原理
首先connect之所以会成功，是因为Provider组件：
* 在原应用组件上包裹一层，使原来整个应用成为Provider的子组件
* 接收Redux的store作为props，通过context对象传递给子孙组件上的connect
