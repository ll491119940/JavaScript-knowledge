#  整理代码

##  JSX

###  多行书写

多行书写元素时，一定要记得用括号封装它们。JSX本质上会替换成函数，由于自动分号插入机制的存在，另起一行的函数可能会导致意外结果。

以下示例可以正常运行，因为div元素和返回在同一行：

`return <div />`

但接下来的示例就失效了：

```react
return
<div />
```

因为它会转化为以下代码：

```javascript
return :
React.createElement("dib", null);
```

因此需要将代码语句包裹在括号内：

```javascript
return (
    <div />
)
```

###  多个属性的书写

常见的解决方案是一行书写一个属性，同时缩进一个层级，并保持结尾扩号和开始标签对齐：

```react
<button
    foo="bar"
    veryLongPropertyName="baz"
    onSomething={this.handleSomething}
/>
```

###  条件语句

当用到条件语句时，JSX可以利用行内条件来判断

```react
<div>
    {isLoggendIn && <LoginButton />}
</div>
```

如果条件语句有额外分支（常见的if...else），并且我们想要在用户登录后显示注销按钮，否则显示登录按钮

更好的替代方案是三元条件运算

```react
<div>
    {isLoggendIn? <LogoutButton /> ：<LogginButton />}
</div>
```

还有一些方案需要用到外部依赖。

第一项 方案是render-if，可以执行以下命令来安装`npm install --save render-if`

```react
const {dataIsReady, isAdmin, userHasPermissions} = this.props
const canShowSecretData = renderIf(
    dataIsReady && (isAdmin || userHasPermissions)
)
<div>
      {canShowSecretData(<SecretData />)}
</div>
```

这个工具函数的返回值也是一个函数，可以接受JSX标记作为参数，当条件为true时显示。

始终牢记，不要在组件内添加过多逻辑。有些组件需要这样做，但我们应该尽量保持组件简洁易懂，这样便于定位和修复问题。

另一个工具库react-only-if，可以执行以下命令来安装这个库：`npm install --save react-only-if`

```react
const SecretDataOnlyIf=onlyIf(
    ({dataIsReady,isAdmin,userHasPermissions}) => {
        return dataIsReady && (isAdmin || userHasPermissions)
    })(SecretData)
<div>
      <SecretDataOnlyIf
          dataIsReady={...}
          isAdmin={...}
          userHasPermissions={...}
      />
</div>
```

在以上代码中，组件内部不包含任何逻辑。将条件语句作为onlyif函数的第一个参数传入，满足条件时就渲染组件。用于校验条件的函数可以接收组件的属性、状态以及上下文环境。这样就可以避免条件语句对组件造成污染，有助于我们更轻松地理解并探究组件的代码。

###  循环

如果在JSX模板中编写一个函数并返回数组，那么数组的每一项都会编译为一个元素。针对给定对象的数组生成元素数组，最常用的做法是使用map方法。

假设有一张用户列表，其中每个用户都有一个对应的姓名属性，用以下代码创建一张无序用户列表

```react
<ul>
    {user.map(user => <li>{user.name}</li>)}
</ul>
```

###  次级渲染

当渲染方法的代码量多到难以维护时，应该怎么做？一种方案是将其拆分成更小的方法，同时又将所有逻辑都保留在原有组件内部。

```react
renderUserMenu() {
    //JSX用于用户菜单
}
renderAdminMenu() {
    //JSX用于管理员菜单
}

render(){
    return (
        <div>
            <h1>Welcome back!</h1>
            {this.userExists && this.renderUserMenu()}
            {this.userIsAdmin && this.renderAdminMenu()}
        </div>
    )
}
```

这种方案并不总是可以当作最佳实践，因为显然拆分组件的做法更好。有时这样做只是为了保持渲染方法简洁。Redux的一个真实示例就是用一个次级渲染的方法来渲染加载更多按钮。

##  ESLint

首先，执行以下命令来安装ESLint

`npm install --global eslint`

安装完成后，可以用以下命令来运行它：`eslint source.js`

###  配置

使用位于项目根目录的.eslintrc文件来配置ESLint，使用rules属性来添加规则。

举例来说，创建.eslintrc文件并禁用分号：

```javascript
{
    "rules": {
        "semi":[2,"never"]
    }
}
```

上述配置文件的含义是：“semi”是规则名，[2,"never"]是规则的值。

ESLint规则具有决定问题严重程度的三个等级。

- off（或者0）：禁用规则
- warn（或者1）：规则会产生警告
- error（或者2）：规则会抛出错误

将规则的值设为2，因为我们希望当代码不符合规则时，ESLint会抛出错误。第二个参数将ESLint配置为不允许代码中使用分号（相反值为always）

可以手动启用或禁用每条规则，也可以一步启用推荐配置，只需要在.eslintrc中添加以下代码即可。

```javascript
{
    "extends": "eslint:recommended"
}
```

no-unused-vars规则对于保持代码简洁非常有用。

最后使用以下配置来启用JSX语法：

```react
"parserOptions": {
    "ecmaVersion":6,
        "ecmaFeatures": {
            "jsx":true
        }
}
```

ESLint可以用插件进行扩展，对我们最重要的一个插件是eslint-plugin-react。ESLint不需要任何插件就能解析JSX，要想使用该插件，需要先进行安装：`npm install --global eslint-plugin-react`

安装完成后，在配置文件中添加以下代码，以便ESLint可以使用它：

```javascript
"plugins" : [
    "react"
]
```

首先，激活以下规则：

```javascript
"rules" : {
    "react/jsx-indent":[2,2]
}
```

第一个2表示如果代码不符合规则，则ESLint应该给出错误提示，第二个2则表示每个JSX元素应该缩进两个空格。

###  Airbnb的配置

React领域最流行的配置之一莫过于Airbnb的那一套，Airbnb的开发者按照React的最佳实践创建了一套规则集，你可以直接在代码库中使用，无须自己手动判断启用哪条规则。

要想使用这套配置，需要安装如下依赖

```javascript
npm install --global eslint-config-airbnbeslint@^2.9.0 eslint-plugin-jsx-a11y@^1.2.0 eslint-plugin-import@^1.7.0 eslint-plugin-react@^5.0.1
```

然后再.eslintrc中添加以下配置：

```javascript
{
    "extends":"airbnb"
}
```

##  函数式编程基础

除了编写JSX时遵循最佳实践，并使用linter来加强代码一致性以更早发现错误，保持代码简洁的另一个方法是：遵循函数式编程风格。

函数式编程就是一种声明式范式，能够避免代码副作用，同时它推崇数据不可变，以便更易维护与考量代码。

###  一等对象

JavaScript的函数是一等对象，这意味着它们可以赋给变量，也可以作为参数传递给其他函数。

高阶函数