<!--
 * @Author: ian.cai
 * @Date: 2023-05-16 14:09:32
 * @LastEditors: ian.cai
 * @LastEditTime: 2023-05-17 16:52:18
 * @Description: 网易云课堂-React完全指南学习笔记
-->
# React完全指南
## 副作用
* 纯函数：传递相同的参数，返回结果相同，且没有其他意外情况出现
* 副作用：改变外部环境

---

## JSX进阶
### 条件渲染的另一种形式
*避免使用三元运算符，逻辑更清晰*

```js
// ...
if (!user) {
  return <div>loadiing...</div>
}
return (
  <Content />
)
```
### 导出子组件：<MyComponent.SubComponent />
```js
// component/Menu.js
import React from 'react';

function Menu({children}) {
  return <nav>{children}</nav>
}

function Item({children}) {
  return <a href='#'>{children}</a>
}

Menu.Item = Item;

export default Menu;
```
```js
// app.js
import Menu from './components/Menu';

function App() {
  return (
    <Menu>
      <Menu.Item>主页</Menu.Item>
      <Menu.Item>关于</Menu.Item>
      <Menu.Item>联系</Menu.Item>
    </Menu>
  )
}

export default App;
```

## React Props进阶
### Render props：给props传递JSX
```js
// components/Layout.js
import React from 'react';

function Layout({nav, children}) {
  return (
    <div className='container'>
      <nav>{nav}</nav>
      <main>{children}</main>
    </div>
  );
}

export default Layout;
```
```js
// index.js
import Layout from './components/Layout.js';

function Nav() {
  return (
    <div>....</div>
  )
}
function App() {
  return (
    <Layout nav={<Nav />}>
      <div>
        <h1>欢迎！</h1>
      </div>
    </Layout>
  );
}

export default App;
```

## React组件进阶
### 组件懒加载：实现代码分割，提高页面加载速度
```js
const About = React.lazy(() => import('./components/About'));

function App() {
  return (
    {showAbout && (
      <Suspense fallback={<div>loading...</div>}>
        <About />
      </Suspense>
    )}
  )
}
```