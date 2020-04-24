---
title: React 之 Render Props
date: 2020-04-24 11:53:52
tags:
    - React
    - Render Props
cover: https://www.pexels.com/zh-cn/photo/3560451/
---

### 什么是 Render Props

Render props 是 React 16 + 之后出现的新特性。 官方是这样解释的:
>“render prop” 是指一种简单的技术，用于使用一个值为函数的 prop 在 React 组件之间的代码共享。

通俗一点解释， 就是一个组件， 接受一个名为render的props属性， render是一个函数， 会在组件render 的时候调用，而不是实现自己的渲染逻辑。

看到这里， 还是有点一头雾水的感觉， react 不是 本来就有组件之间的封装和嵌套吗，为什么非要通过这种方式给一个组件注入另一个组件的代码呢？官方是这样解释的:
>render prop 是一个组件用来了解要渲染什么内容的函数 prop。

所以， 再通俗的解释， 当一个组件的基础功能是提供“可变数据”， 不知道自己需要渲染什么东西的时候， 具体的展示可以从外部注入。

我们可以通过下面的例子来加深理解

### Render Props的使用

假设目前有这样的一个需求，有一个后台管理系统， 里面有很多功能结构类似的列表， 每个列表都是进入页面后请求接口， 然后根据获取到的数据对列表进行渲染， 然后列表还包括一些简单的排序， 分页等功能。

这种最简单的实现方式就是在每个列表中把这些功能都实现一遍。

实现方式：

```
// list A
class ListA extends Components {
    // 列表通用逻辑
    handleSearch = () => {}
    handleChangePage = () => {}
    ...

    render() {
        const { list } = this.state;
        return (
            <div>
            // 列表A渲染
            </div>
        )
    }
}
// list B, list C, ....
```

在上面的例子中， 列表获取、分页、筛选等功能都是相同的，没有必要再使用的时候一遍又一遍的重复写这些逻辑。
如果能把这些逻辑提取成公共组件的话， 那样就完美了。
可是如果提取成公共组件的话， 每个列表的渲染是不同的， 这段是不能被封装进公共部分。

这个时候， 就可以使用 `Render Props` 了. 我们可以提供一个带有函数props 的ConmmonList 组件， 他能够根据我们的需要进行动态渲染。

实现方式：

```
class ConmmonList extends Components {
    // 列表通用逻辑
    handleSearch = () => {}
    handleChangePage = () => {}
    ...

    render() {
        const { list, render } = this.state;
        return { this.props.render(list) }
    }
}

class ListA extends Components {
    render() {
        return <ConmmonList render={(list) => (<ListARender list={list} >)}
    }
}

class ListB extends Components {
    render() {
        return <ConmmonList render={(list) => (<ListBRender list={list} >)}
    }
}
```

`render props` 的好处在于， 不需要通过“混入”或者装饰来共享组件行为，一个普通组件只需要一个函数 prop 就能够进行一些 state 共享。

子组件（上例中的ConmmonList） 通过 render 方法将自己的state暴露给了父组件（ListA, listB）, 我们就可以在父组件中随意使用这个state， 组件之间的通信变得简单并且优雅。


### 使用 Props 而非 render

我们只是把这种模式成为 `render props`, 传入组件中的props 不一定非要叫 render，换成 childer或者其他的名字都可以。

既然说到了`children`, 那么这个children和普通的children有什么不一样呢，  普通的children的使用：

```
render() {
    return <div>{this.props.children}<div>
}
```

普通的children 是一个react element， 不需要函数调用， 可以直接使用， 但是如果我们使用 `render props`， 那么传入的 children 是一个函数， 所以最好在propTypes 里声明 children 应为一个函数类型。

```
Mouse.propTypes = {
  children: PropTypes.func.isRequired
};
```

### 警告: 在 React.PureComponent 中使用 render props 要注意

我们在`render props` 时， 每次向子组件（上例中的 commonList）中传入的render函数 是一个匿名函数， 如果子组件（commonList）使用了react.pureComponent,  因为pureComponent 是进行了浅比较， 所以每次新的匿名函数和上次都不会相等， 那么组件每次都会重新render，pureComponent 也就不会生效了

解决方法： 把render方法也用变量存一下就可以了

```
class ListA extends Components {
    renderList = (list) => (<ListARender list={list} >);
    render() {
        return <ConmmonList render={this.renderList}
    }
}
```



