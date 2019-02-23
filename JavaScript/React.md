

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

**高阶函数**

高阶函数接受一个函数作为参数，也可以传入其他参数，最后返回另一个函数。返回的函数通常会添加一些增强的特殊行为。

```react
//如下示例，一个两数相加的函数在增强后先打印所有参数，再接着执行原先的逻辑
const add = (x,y) => x + y
const log = func => (...args) => {
    console.log(...args)
    return func(...args)
}
const logAdd = log(add)
```

理解这个概念非常重要，因为React领域的一个常用模式是使用高阶组件，将组件当作函数，并为它们增加一些常用行为。

###  纯粹性

编写 纯粹函数是函数式编程的一个重要方面。

纯粹函数是指它不产生副作用，也就是说它不会改变自身作用域以外的任何东西。举例来说，如果函数改变了应用状态、修改了上层作用域定义的变量，或者与DOM这样的外部实体发生了交互，那么该函数就是非纯粹函数。

以下展示的就是纯粹函数

`const add = (x, y) => x + y`

它可以运行多次，并且总能得到同样的结果，因为没有将数据存储在其他地方，也没有修改任何东西。

###  不可变性

在函数式编程中，函数不会修改变量值，而是创建新的变量，赋新值后再返回变量。操作数据的这种方式称为不可变性。

不能修改不可变值

###  柯里化

柯里化是函数式编程的常用技巧。柯里化过程就是将多参数函数转换成单参数函数，这些单参数函数的返回值也是函数。

我们从前文的add函数入手，将它转换成柯里化函数

```javascript
//原先的写法如下所示
const add = (x, y) => x + y
//将其定义为以下写法
const add = x => y => x + y
```

###  组合

最后，可以用于React的函数式编程中的另一个重要概念是组合。函数（和组件）可以结合产生新函数，从而提供更高级的功能与属性

###  函数式编程与UI

可以将UI看作传入应用状态的函数，`UI = f(state)`

使用React时，可以将创建UI的组件看作函数，组件可以组合形成最后的UI，这也正是函数式编程的特性之一。

#  开发真正可复用的组件

React引入了一种新型组件，允许将组件定义为无状态函数。

##  创建类

###   createClass 工厂方法

先从一段很简单的代码开始：

```react
const Button = React.createClass({
    render() {
        return <button />
    },
})
```

以上代码创建了一个按钮组件，并且应用的其他组件也可以引用它。

###  继承React.Component

用类重写上例中的按钮：

```react
class Button extends React.Component {
    render() {
        return <button />
    }
}
```

###  主要区别

除了语法方面的差异，上述两种方法还有以下几项主要区别：

**prop**

第一个区别在于如何定义组件期望接收的prop及其默认值。

`createClass`方法需要在作为参数传入函数的对象内定义prop，同时在`getDefaultProps`内返回默认值：

```javascript
const Button = React.createClass({
    propTypes：{
    	text: React.PropTypes.string,
	},
    getDefaultProps() {
		return{
        	text: 'Click me!'
        }                                                          
	},
    render(){
        return <button>{this.props.text}</button>
    },
})
```

以上代码中，用propTypes属性列出了能够传递给组件的所有prop。用`getDefaultProps`函数定义了prop的默认值，如果父组件中传递了prop，那么对应的默认值会被覆盖。

如果用类实现同样目的，则需要用到稍微不同的结构：

```react
class Button extends React.Component {
    render() {
        return <button>{this.props.text}</button>
    }
}
Button.propTypes = {
    text:React.PropTypes.string,
}
Button.defaultProps = {
    text: 'Click me!',
}
```

在设置默认的prop时，我们原先用函数来返回默认属性对象，但在使用类时，需要在类上定义defaultProps属性，再将默认值对象赋给它。

使用类的好处在于，只需要在JavaScript对象上定义属性，无须使用`getDefaultProps`这种React特有的函数

**状态**

另一个重大区别是，组件初始状态的定义方式不同。

```javascript
const Button = React.createClass({
    getInitialState() {
        return {
            text:'Click me!',
        }
    },
    render() {
        return <button>{this.state.text}</button>
    },
})
```

`getInitialState`方法期望返回一个对象，该对象包含每个状态属性的默认值。

如果用类来定义初始状态，则需要在累的构造器方法内设置实例的状态属性：

```react
class Button extends React.Component {
    constructor(props) {
        super(props)
        
        this.state = {
            text: 'Click me!',
        }
    }
    
    render() {
        return <button>{this.state.text}</button>
    }
}
```

定义状态的这两种方式等效，不过使用类的好处与前面一样，无须使用React特有的API

**自动绑定**

`createClass`有一项非常方便的特性，允许我们创建事件处理器，并且当调用事件处理器时，this会指向组件本身。

```react
const Button = React.createClass({
    handleClick() {
        console.log(this)
    },
    render() {
        return <button onClick={this.handleClick} />
    },
})
```

`createClass`允许我们按照以上方式设置事件处理器，这样一来，函数内部的this就会指向组件本身。这允许我们调用同一组件实例的其他方法。例如调用`this.setState()`或者其他方法所产生的结果都能符合预期。

按照以下方式继承`React.Component`并定义组件

```react
class Button extends React.Component {
    handleClick() {
        console.log(this)
    }
    
    render() {
        return <button onClick={this.handleClick} />
    }
}
```

单击按钮后，控制台输出的结果为null。这是因为函数传给事件处理器后丢失了对组件的引用。

这并不意味着不能在类中使用事件处理器，只是我们‘需要手动绑定函数。

解决自动绑定的一种方案就是箭头函数

```react
class Button extends React.Component {
    handleClick() {
        console.log(this)
    }
    
    render() {
        return <button onClick={() => this.handleClick()} />
    }
}
```

这样做符合预期，也不会带来什么特殊问题。唯一的缺点在于，如果在意性能，那么就需要理解代码的本质。实际上，在渲染方法中绑定函数会带来无法预料的副作用，因为每次渲染组件时都会触发箭头函数。如果这个函数传递给子组件，那么子组件在每次更新过程中都会接收新的prop。这可能会导致低效的渲染，进而引发问题，对于纯粹组件而言尤其如此。

解决函数绑定问题的最佳方案是在构造器内进行绑定操作，这样即使多次渲染组件，它也不会发生任何改变。

```react
class Button extends React.Component {
    constructor(props){
        super(props)
        this.handleClick = this.handleClick.bind(this)
    }
    handleClick() {
        console.log(this)
    }
 
    render() {
        return <button onClick={this.handleClick} />
    }
}
```

###  无状态函数式组件

`() => <button />`

以上代码创建了一个空按钮，简洁的箭头函数语法使得其代码变得直观且极具表现力。

1. props与上下文

不能从父组件接收props对象的组件没有多大用处，而无状态函数式组件可以接收props对象作为参数：

`props => <button>{props.text}</button>`

还可以使用ES6语法：`({text}) => <button>{text}</button>`

定义props后，像继承组件那样，无状态函数就可以通过propTypes属性接收props：

```react
const Button = ({text}) => <button>{text}</button>
Button.propTypes = {
    text: React.PropTypes.string,
}
```

无状态函数式组件也接收表示上下文的第二个参数

`(props, context) => (<button>{context.currency}{props.value}</button>)`

2. 关键词this

无状态函数式组件与状态组件的一项区别在于，this在无状态函数式组件的执行过程中不指向组件本身。由于这个原因，与组件实例相关的setState等方法以及生命周期方法都无法使用。

3. 状态

无状态函数式组件没有任何内部状态，这正是因为this不存在所导致的。这使得无状态函数式组件无比强大，同时又很容易使用。无状态函数式组件只接收props（以及上下文）参数，并返回相应元素。

4. 生命周期

无状态函数式组件没有提供任何像`componentDidMount`这样的生命周期钩子；它们只实现了一个类似渲染的方法，并将其他工作都交由父组件来执行。

5. ref与事件处理器

因为无状态函数式组件不能访问组件实例，所以如果要使用ref或者事件处理器，需要按以下方式来定义。

```react
() => {
    let input
    const onClick = () => input.focus()
    return (
        <div>
            <input ref={el => (input = el)} />
            <button onClick = {onClick}>Focus</button>
        </div>
    )
}
```

6. 没有组件引用

无状态函数式组件的另一个不同点在于，无论何时使用ReactTestUtils来渲染它们，都无法取回对组件的引用。

```react
const Button = React.createClass({
    render() {
        return <button />
    }
})

const component = ReactTestUtils.renderIntoDocument(<Button />)
//以上示例中，组件表示Button

const Button = () => <button />
const component = ReactTestUtils.renderIntoDocument(<Button />)
//但这个示例中的组件为null，将组件包裹在一个div标签中是一种解决方案
const component = ReactTestUtils.renderIntoDocument(<div><Button /></div>)
```

7. 优化

因为没有shouldComponentUpdate方法，所以无法通知React只在props变化时才渲染函数式组件

##  状态

###  外部库

大部分React教程或者构建模板都包括了管理应用状态的外部库，如Redux或Mobx。本节的目的就是弄清楚如何正确使用状态，并理解为何某些情况下不需要任何外部库。

###  工作原理

除了工厂方法和继承Component声明初始状态的方式不同，我们学习的另一个重要概念是，每个有状态的React应用都可以拥有初始状态。

在组件的生命周期中，可以使用生命周期方法或者事件处理器中的setState多次修改状态。当状态发生变化时，React就用新状态渲染组件，这也是文档经常提到React组件类似状态机的原因。用新状态调用setState方法时，对象会合并到当前状态上。

```react
//假设初始状态如下所示：
this.state = {
    text: 'Click me!',
}
//接着用新参数调用setState：
this.setState({
    cliked:true,
})
//最终状态如下
{
    cliker:true,
    text:'Click me!',
}
```

当状态发生改变时，React会再次执行渲染方法，因此除了设置新状态，我们不用做任何事。然而某些情况下可能需要在状态更新完成时执行一些操作，React为此提供了一个回调函数：

```react
this.setState({
    clicked: true,
}, () => {
    console.log('the state is now', this.state)
})
```

将任意函数作为setState的第二个参数传递，状态更新完成时会触发该函数，同时组件完成渲染。

###  异步

应该总是将setState方法当作异步的，实际上，如果在事件处理器中触发了setState后，尝试将当前状态值打印到控制台中，那么获得的是旧状态值：

```react
handleClick() {
    this.setState({
        clicked:true,
    })
    console.log('the state is now', this.state)
}
render(){
    return <button onClick={this.handleClick}>Click me!</button>
}
```

上述代码将会输出 the state is now null。发生这种情况的原因在于React知道如何优化事件处理器内部的状态更新，并进行批处理，以获得更好的性能。

###  React lumberjack

React的工作方式很像状态机，每当状态改变就重新渲染。得益于这个特点，我们可以应用或撤销状态变化，并在整个过程中前进或者后退，这对调试很有帮助。react-lumberjack的使用非常简单，不过要记得在生产环境中禁用它。它可以使用npm导入，也可以直接按以下方式引用它：

`<script src="https://unpkg.com/react-lumberjack@1.0.0"></script>`

脚本加载完成后，只需要使用应用让组件修改自身的状态即可。如果某个地方出错或者想要调试应用的某个特殊状态，可以打开控制台并输入以下代码：

`Lumberjack.back()`

上述代码可以在时间上回退并撤销状态的改变，再查看以下代码：

`Lumberjack.forward()`

上述代码可以在时间上前进并重新应用状态的改变。

###  使用状态

应该牢记只能将满足需求的最少数据放到状态中。只将记录当前UI所需的信息保存到状态中，如标签菜单的当前选中项。判断状态是否适合保存信息的另一种方式是检查组件外部或子组件是否需要我们所维护的数据。如果多个组件都需要跟踪同一份信息，那么应该考虑使用应用层级的状态管理器，如Redux。

接下来我们将看看哪些情况下应该避免使用状态，以遵循最佳实践指南。

1. 可派生的值

只要能根据props计算最终值，就不应该将任何数据保存在状态中。例如，如果从props接收了货币单位及价格，且总要一同展示它们，那么我们可能会认为将它保存在状态中更好，并在渲染方法内使用状态值，如下所示：

```react
class Price extends React.Component {
    constructor(props){
        super(props)
        this.state = {
            price: `${props.currency}${props.value}`
        }
    }
    render(){
        return <div>{this.state.price}</div>
    }
}
```

问题在于，如果货币单位或价格在Price组件的生命周期内发生改变，则永远不会重新计算状态（因为只会调用构造器一次），应用就会显示错误的价格。因此，只要可以，就应该用props来计算值。

可以直接在渲染方法中使用一个辅助函数：

```react
getPrice() {
    return `${this.props.currency}${this.props.value}`
}
```

2. 渲染方法

始终牢记，设置状态会触发组件的重新渲染。因此，应该只将渲染方法要用到的值保存在状态中。

##  prop类型

我们的目的是开发真正可复用的组件，为了实现这一目的，需要尽可能清晰地定义组件接口。如果希望整个应用可以复用组件，关键要确保清晰地定义组件及其参数。React提供了一个可以非常简单地表达组件接口的强大工具，只要提供组件期望接收的prop名称与对应的验证规则即可。与属性类型相关的规则也包含该属性为必选还是可选，还提供了用于编写自定义验证函数的选项。

```react
const Button = ({text}) => <button>{text}</button>
Button.propTypes = {
    text: React.PropTypes.string,
}
```

以上代码创建了一个无状态函数式组件，以接收一个类型为字符串的文本prop。

有时仅添加属性还不够，因为无法告知我们没有该属性时组件能否正常工作。例如没有文本的情况下，按钮组件无法正常操作，解决方法就是将该prop标记为必需：

```react
Button.propTypes = {
    text: React.PropTypes.string.isRequired,
}
```

需要强调的是，这种警告只会在开发模式下出现。生产版本的React出于性能原因禁用了propTypes验证。React提供了多种开箱即用的验证器：从数组到数字类型，再到组件类型。它还提供了oneOf这样的工具函数，以接受对某个特定属性有效的类型数组。记住，我们应该始终将基本类型的prop传给数组，因为它们更容易验证和比较。传递单一基本类型的prop有助于判断组件接口是否过泛，以及是否应该对其进行拆分。

然而某些情况下不可避免地要传递对象，此时需要用模型来定义propType。模型函数允许我们声明包含嵌套属性的对象，并为每个属性定义类型。举例来说，如果要创建Profile组件，且该组件需要传入用户对象，其中包括必需的名字属性以及可选的姓氏属性，则可以按照以下方式定义：

```react
const Profile = ({user}) => (
    <div>{user.name} {user.surname}</div>
)
Profile.propTypes = {
    user: React.PropTypes.shape({
        name: React.PropTypes.string.isRequired,
        surname:React.PropTypes.string,
    }).isRequired,
}
//如果React现有的propTypes无法满足需求，那么我们可以创建自定义函数来验证属性
user: React.PropTypes.shape({
    age:(props, propName) => {
        if(!props[propName] > 0 && props[propName] < 100) {
            return new Error(`${propName} must be between 1 and 99`)
        }
        return null
    },
})
```

例如，上述代码段验证了年龄字段是否属于特定区间；如果不属于，则返回错误。

**React Docgen**

得益于prop类型，组件的边界已经定义得很清晰了，我们还可以进行另一个操作，以便它们更易使用和共享。可以从prop类型的定义起步，自动为组件生成文档。

react-docgen库可以实现这个目的，执行以下命令来安装这个库：`npm install --global react-docgen`

React Docgen会读取组件的源代码，并从prop类型及其注释中提取相关信息。

例如最初创建按钮组件的示例：

```react
const Button = ({text}) => <button>{text}</button>

Button.propTypes = {
    text:React.PropTypes.string,
}
```

接着执行以下代码：`react-docgen button.js`

最后会得到以下对象

```json
{
    "description": "",
    "method": [],
    "props": {
        "text": {
            "type": {
                "name": "string"
            },
            "required": false,
            "description": ""
        }
    }
}
```

以上的JSON对象表示组件的接口。其中props属性包括了类型为字符串的文本属性。

现在可以利用返回的对象来创建文档，并与团队成员共享或发布到GitHub。用docgen提供组件文档的用例可以参加优秀的Material UI库，其所有文档都是根据源代码自动生成的。

##  可复用组件

现在我们来看一个真实示例，研究如何将一个不可复用的组件改成接口清晰通用的可复用组件。

假设组件从API路径加载一个消息集合，并在屏幕上显示列表。

```react
//组件的定义方式如下所示
class PostList extends React.Component {
    //其中包括构造器和一个生命周期方法
    constructor(props) {
        super(props)
        this.state = {
            posts: [],
        }
    }
    componentDidMount() {
        Posts.fetch().then(
            posts => {
                this.setState({posts})
            }
        )
    }
}
```

一个空数组被赋给消息，以表示初始状态。调用componentDidMount时会触发API调用，取回的数据将保存到状态中。这种数据获取模式相当常见。辅助类Posts用来与API通信，它的获取方法会返回一个Promise对象，请求成功后会返回消息列表。

现在我们来看看显示消息列表部分的代码

```react
render() {
    return (
        <ul>
            {this.state.posts.map(post => (
                <li key={post.id}>
                    <h1>{post.title}</h1>
                    {post.excerpt && <p>{post.excerpt}</p>}
                </li>
            ))}
        </ul>
    )
}
```

我们在render方法内遍历了消息，并将其中的每条消息都映射为`<li>`元素。假设始终需要显示标题字段，并将它包裹在`<h1>`标签中，而摘要属性是可选的，如果存在，就显示在段落中。

上述组件可以正常工作，而且没有任何问题。现在，假设我们需要渲染一个类似的列表，不过这次想要显示的是从props而不是状态中获取的用户列表（以明确表示我们能应对不同场景）：

#  组合一切

##  函数子组件

React社区目前对一种名为函数子组件的模式达成共识。

这种模式的主要概念是，不按组件的形式传递子组件，而是定义一个可以从父组件接收参数的函数。

```react
const FunctionAsChild = ({children}) => children()
FunctionAsChild.propTypes = {
    children:React.PropTypes.func.isRequired,
}
```

FunctionAsChild组件拥有定义为函数的children属性，并且它没有按JSX表达式的形式使用，而是作为函数被调用。

上述组件的用法如下所示：

```react
<FunctionAsChild>
    {() => <div>Hello,World!</div>}
</FunctionAsChild>
```

父组件的渲染方法触发了子函数，返回了div标签包裹的Hello，World！文本，最后显示在屏幕上。

#  恰当地获取数据

##  数据流

React推行了一种非常有趣的模式，允许数据从根节点流向叶节点。这种模式通常称作单向数据流。

顾名思义，React中的数据流是单向的，即从组件树的顶部流向底部。这种方式有很多好处，它简化了组件行为以及组件间的关系，增强了代码的可预测性和可维护性。

每个组件都以prop的形式从父组件接收数据，并且prop无法修改。获取数据后，可以将其转换为新的形式或者往下传给其他子组件。每个字组件都能保存内部状态，也可以将状态作为自身嵌套组件的prop。

我们来探讨Counter组件的代码，该组件从0开始计数且拥有两个按钮，分别用于计数器值的增和减。

```react
class Counter extends React.Component{
    //该类在构造器中将计数器初始化为0，并在组件自身上绑定了事件处理器
    constructor(props){
        super(props)
        
        this.state = {
            counter:0,
        }
        this.handleDecrement = this.handleDecrement.bind(this)
        this.handleIncrement = this.handleIncrement.bind(this)
    }
    //事件处理器的代码很简单，它们只是修改了状态，增加或减少当前的计数
    handleDecrement(){
        this.setState({
            counter:this.state.counter - 1,
        })
    }
    handleIncrement(){
        this.setState({
            counter:this.state.counter + 1,
        })
    }
    //最后，在渲染方法中显示当前值，每个按钮的onClick属性定义好各自的处理器
    render(){
        return(
            <div>
                <h1>{this.state.counter}</h1>
                <button onClick={this.handleDecremenr}>-</button>
                <button onClick={this.handleIncremenr}>+</button>
            </div>
        )
    }
}

```

###  子组件与父组件的通信（回调函数）

当子组件需要向父组件推送信息或触发事件时，React通常采用回调函数来实现。

先创建Buttons组件来显示增减按钮。当点击按钮时，不再触发内部函数，而是触发props上传来的函数。

```react
const Buttons = ({onDecrement, onIncrement}) => (
    <div>
        <button onClick={onDecrement}>-</button>
        <button onClick={onIncrement}>+</button>
    </div>
)
Buttons.propTypes = {
    onDecrement:React.PropTypes.fuc,
    onIncrement:React.PropTypes.fuc,
}
```

用新组件替换原有标记即可，并将内部函数传给它

```react
render(){
    return(
        <div>
            <h1>{this.state.counter}</h1>
            <Buttons 
                onDecrement={this.handleDecrement}
                onIncrement={this.handleIncrement}
            />
        </div>
    )
}
```

其他部分都保持原样，逻辑仍然位于父组件中。

每当子组件需要向父组件推送数据或者通知父组件发生了某个事件时，可以传递回调函数，同时将其余逻辑放在父组件中。

###  公有父组件

抽离显示逻辑，创建一个Display组件来接收所需的值并在屏幕上显示出来

```react
const Display = ({counter}) => <h1>{counter}</h1>

Display.propTypes = {
    counter:React.PropTypes.number,
}
```

在Counter中使用新组件，用Display组件替换旧标记即可

```react
render(){
    return(
        <div>
            <Display counter={this.state.counter} />
            <Buttons 
                onDecrement={this.handleDecrement}
                onIncrement={this.handleIncrement}
            />
        </div>
    )
}
```

两个兄弟组件通过公有父组件进行了通信。当被点击时，Buttons组件会通知父组件，然后父组件会将更新后的值发送给Display组件。这种模式在React中很常见，而且它可以有效地在没有直接联系的组件间共享数据。

数据始终从父组件流向子组件，但子组件可以发送通知给父组件，以便组件树按照新的数据重新渲染。

每次需要让两个没有关联的组件相互通信时，都要找到它们的公有父组件来保存状态。这样一来，当状态更新时，两个组件都能从props接收新数据。

##  数据获取

我们要构建的第一个组件是一个简单的gist列表

```react
class Gists extends React.Component{
    constructor(props){
        super(props)
        
        this.state = { gists:[] }
    }
    //用于获取数据的代码可以放在两个生命周期钩子中：componentWillMount和componentDidMount
    //前者会在组件首次渲染前触发，后者在组件挂载完成后立即触发。但服务端渲染和客户端渲染都会触发componentWillMount函数。当服务端渲染组件时，触发异步API会带来意料之外的结果，顾只能用componentDidMount钩子，这样就能确保只在浏览器端调用API请求
    componentDidMount(){
        fetch('https://api.github.com/users/gaearon/gists')
        .then(response => response.json())
        .then(gists => this.setState({gists}))
    }
    
    render(){
        return(
            <ul>
                {this.state.gists.map(gist => (
                    <li key={gist.id}>{gist.description}</li>
                ))}
            </ul>
        )
    }
}

```

组件可以工作正常，不过正如之前所说，我们可以将渲染逻辑放入一个独立的子组件，以便它更简洁，便于测试。

现在，常见的一个需求是多处代码都要从API获取数据，但我们并不想复制代码。要想从组件中移除数据逻辑并在整个应用中复用，其中一个解决方案就是创建高阶组件。高阶组件会代替增强后的组件来加载数据，然后以prop的形式向子组件提供数据。

先通过偏函数写法接受其他参数，然后将实际组件作为第二个参数：

```react
const withData = url => Component => (...)
```

该函数的参数为获取数据的URL以及所需数据的组件。该函数返回的类如下所示：

```react
class  extends React.Component{
    constructor(props){
        super(props)
        //此处用于保存数据的属性名为data，因为我们要开发通用组件，不希望它只能绑定某种特定格式的对象或集合。
        this.state = { data:[] }
    }
    //componentDidMount钩子触发获取函数，将服务端返回的数据转换成JSON对象并保存在状态中
    componentDidMount(){
        fetch(url)
        .then(response => response.json())
        .then(data => this.setState({data}))
    }
    //现在使用高阶组件传入的第一个参数来设置URL，最后为了使高阶组件更加直观，渲染给定组件时展开props对象。同时展开状态，以便向子组件传递JSON数据
    render(){
        return <Component {...this.props}{...this.state} />
    }
}
```

现在我们可以封装应用的任何组件，为它们提供从任何URL获取的数据。

首先创建一个不含数据获取逻辑的组件，它只负责接收数据并像最初示例那样用标记显示出来：

```react
const List = ({data: gists}) => (
    <ul>
        {gists.map(gist => (
            <li key={gist.id}>{gist.description}</li>
        ))}
    </ul>
)

List.propTypes ={
    data:React.PropTypes.array,
}
```

接着我们来看如何使用高阶组件withData，使其将数据传给刚刚创建的List组件。我们可以先定制高阶组件来发起特定请求，然后多次复用它。

```react
const withGists = withData('https://api.github.com/users/gaearon/gists')
```

这种做法秒在可以用新的withGists函数封装任何组件，不用重复指定URL就可以接收gaearon的gist列表。

最后，封装组件并获得新组件：

```react
const ListWithGists = withGists(List)
```

遗憾的是，在使用高阶组件时prop是未知的，因此在发起API请求前，一旦获取prop就需要触发某个钩子函数。

可以修改高阶组件，让它接受两种类型的URL参数：一种是当前实现的字符串类型，另一种是函数，它接受组件的prop并根据传入的参数返回URL。

```react
componentDidMount(){
    const endpoint = typeof url === 'function' ? url(this.props) : url
    fetch(endpoint)
    .then(response => response.json())
    .then(data => this.setState({data}))
}
```

如果URL是函数，就以props为参数来执行它；如果URL是字符串，那么就直接使用。

```react
const withGists = withData(
    props => `https://api.github.com/users/${props.username}/gists`
)

//可以在组件的prop中设置username参数，用于加载gist
<ListWithGists username="gaearon" />
```

##  react-refetch

我们可以用`react-refetch`实现上面同样的目的。

首先，安装这个库：`npm install react-refetch --save`

接着导入该模块的connect函数

`import {connect} from 'react-refetch'`

最后，用connect这个高阶组件装饰原有组件。我们利用偏函数技巧将该函数特殊化，然后再复用它：

```react
const connectWithGists = connect(({username}) => ({
    gists:`https://api.github.com/users/${username}/gists`,
}))
```

我们将一个函数作为参数传入connect函数。参数函数接受props（以及context）作为参数，这样就能根据组件的当前属性创建动态的URL。传入的回调函数返回一个对象，该对象的键名标识相应的请求，键值就是URL路径。URL并不局限于字符串形式。

现在，可以用刚刚创建的函数来增强组件

```react
const ListWithGists = connectWithGists(List)
```

原有组件需要稍作改动才能用于新的高阶组件。首先，参数名不再是data，而是gists。实际上，react-refetch库注入的属性与我们在connect函数中指定的键同名。gist prop并不是真正的数据，而是一种名为PromiseState的特殊对象。PromiseState对象是Promise的同步表示，并且它具备一些很有用的属性，如pending和fulfilled，可以利用这两个属性显示加载动画或数据列表。它还有一个用于处理异常情况的rejected属性。

当请求变成已满足状态时，可以通过value属性访问需要加载得数据，并遍历它来显示gist列表：

```react
const List = ({gist}) => (
    gists.fulfilled && (
        <ul>
            {gists.value.map(gist => (
                <li key={gist.id}>{gist.description}</li>
            ))}
        </ul>
    )
)
//另外，还需要更新组件的propTypes，并修改所接收prop的名称和类型：
List.propTypes ={
    gists: React.PropTypes.object,
}
```

既然项目引入了这个库，我们可以为List组件添加更多功能。举例来说，可以添加按钮来为gist加星。先从UI着手，然后利用react-refetch库添加真正的API请求。我们不希望在List组件中增加过多功能，因为其职责就是显示列表。因此，改用子组件渲染每一行。新组件命名为Gist，我们将它用在循环内部，如下所示

```react
const List = ({gist}) => (
    gists.fulfilled && (
        <ul>
            {gists.value.map(gist => (
                <Gist key={gist.id} {...gist} />
            ))}
        </ul>
    )
)
```

用Gist组件替换`<li>`元素即可，接着展开gist对象并传给组件，这样它就能接受单个属性，测试和维护也更加方便。

组件接受description

属性，并且目前与原有标记的区别仅在于多了一个+1按钮。接下来我们将给这个按钮添加一些功能：

```react
const Gist = ({description}) => (
    <li>
        {description}
        <button>+1</button>
    </li>
)

Gist.propTypes = {
    description:React.PropTypes.string,
}
```

为gist加星的URL路径是

`https://api.github.com/gists/:id/star?access_token=:access_token<>`

下一步是在按钮的onClick事件上添加函数，以便用gist的ID调用API

react-refetch库的connect函数接受一个函数作为第一个参数。这个函数需要返回包含请求的对象。如果这些请求的值是字符串，那么取得prop后就会立马开始获取数据，如果某个请求的值是函数，那么它会传递给组件，并且可以延迟触发。

```react
const token='access_token=123'
const connectWithStar = connect(({id}) => ({
    star:() => ({
        starResponse:{
            url:`https://api.github.com/gists/${id}/star?${token}`,
            method:'PUT',
        },
    }),
}))
```

现在是时候增强组件了：

`const GistWithStar = connectWithStar(Gist)`

同时在组件内用star函数发起请求：

```react
const Gist = ({description, star}) => (
    <li>
        {description}
        <button onClick={star}>+1</button>
    </li>
)

Gist.propTypes = {
    description:React.PropTypes.string,
    star:React.PropTypes.func,
}
```

组件接收star函数，star就是我们在connect函数中定义的请求名称。点击按钮时触发该函数。

#  为浏览器编写代码

##  表单

###  自由组件

我们从一个最基本的示例开始：显示一张包含输入框和提交按钮的表单。

```react
const Uncontroll = () => (
    <form>
        <input type="text" />
        <button>Submit</button>
    </form>
)
```

本例展示的就是一个自由组件，我们没有在该组件中设置输入框的值，而是让组件自己管理内部状态。大多数情况下，当提交按钮被点击时，我们想要对输入框元素的值进行操作。

实现这个需求很简单，添加onChange监听器即可。

首先，因为需要定义状态和一些函数，所以先将组件从无状态函数改写为类：

```react
class Uncontroll extends React.Component{
    constructor(props){
        super(props)
        this.handleChange = this.handleChange.bind(this)
    }
    //定义事件监听器
    handleChange({target}){
        console.log(target.value)
    }
    //渲染表单
    render(){
        return(
            <form>
        		<input type="text" onChange={this.handleChange} />
        		<button>Submit</button>
    		</form>
        )
    }
    
}
```

每当输入框的值改变时，就会触发handleChange监听器。因此，每输入一个字符就会调用一次监听函数。下一步是将用户输入的值保存进状态，以便点击提交按钮时可以获取。

接着修改处理器的实现，移除控制台打印的代码并将值保存进状态

```react
class Uncontroll extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            value: '',
        }
        //构造器中增加第二个事件处理器
        this.handleChange = this.handleChange.bind(this)
        this.handleSubmit = this.handleSubmit.bind(this)
    }
    //定义事件监听器
    handleChange({target}){
    	this.setState({
        	value:target.value,
    	})
	}
    //定义handleSubmit函数
    handleSubmit(e){
        e.preventDefault()
        console.log(this.state.value)
    }
    //渲染表单
    render(){
        return(
            <form>
        		<input type="text" onChange={this.handleChange} />
        		<button>Submit</button>
    		</form>
        )
    }
    
}

```

接着创建一张包含姓和名两个输入框的新表单。

```react
class Uncontroll extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            firstName: '',
            lastName: '',
        }
        //构造器中增加第二个事件处理器
        this.handleChangeFirstName = this.handleChangeFirstName.bind(this)
        this.handleChangeLastName = this.handleChangeLastName.bind(this)
        this.handleSubmit = this.handleSubmit.bind(this)
    }
    //定义事件监听器
    handleChangeFirstName({target}){
    	this.setState({
        	firstName:target.value,
    	})
	}
    handleChangeLastName({target}){
    	this.setState({
        	lastName:target.value,
    	})
	}
    //定义handleSubmit函数
    handleSubmit(e){
        e.preventDefault()
        console.log(`${this.state.firstName}${this.state.lastName}`)
    }
    //渲染表单
    render(){
        return(
            <form onSubmit={this.handleSubmit}>
        		<input type="text" onChange={this.handleChangeFirstName} />
                <input type="text" onChange={this.handleChangeLastName} />
        		<button>Submit</button>
    		</form>
        )
    }
    
}

```

接下来我们看看如何对它稍作优化。我们的基本目的是使用单个改变处理器，这样不用创建新监听器就能添加任意数量的输入框

```react
class Uncontroll extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            firstName: '',
            lastName: '',
        }
        //在构造器中定义单个改变处理器
        this.handleChange = this.handleChange.bind(this)
        this.handleSubmit = this.handleSubmit.bind(this)
    }
    //如何修改onChange的实现，以便它能处理不同的输入框
    handleChange({target}){
    	this.setState({
        	[target.name]:target.value,
    	})
	}
    //事件对象的目标属性表示触发事件的输入框。因此，我们可以将输入框名称及其值作为变量。
    //定义handleSubmit函数
    handleSubmit(e){
        e.preventDefault()
        console.log(`${this.state.firstName}${this.state.lastName}`)
    }
    //渲染表单
    render(){
        return(
            <form onSubmit={this.handleSubmit}>
        		<input type="text" name="firstName"onChange={this.handleChange} />
                <input type="text" name="lastName"onChange={this.handleChange} />
        		<button>Submit</button>
    		</form>
        )
    }
    
}
```

现在可以添加任意数量的输入框，而无须创建额外的处理器。

###  受控组件

下一步要学习的是如何用某些值预置表单元素，可以从服务端接收这些值，也可以通过props从父组件接收。

以下第一个示例展示了输入框内部的预定义值：

```react
const Controlled = () => (
    <form>
        <input type="text" value="Hello React" />
        <button>Submit</button>
    </form>
)
```

在浏览器中运行该组件就会发现，它按预期显示了默认值，但不允许我们修改这个值，也不能输入任何字符。

如果我们希望输入框有默认值，并且输入时可以改变这个值，那么可以使用defaultValue属性

```react
const Controlled = () => (
    <form>
        <input type="text" defaultValue="Hello React" />
        <button>Submit</button>
    </form>
)
```

但我们想要完全掌控组件值，为此，应该将组件从无状态函数改写成类

```react
class Controlled extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            firstName: 'Dan',
            lastName: 'Abramov',
        }
        //在构造器中定义单个改变处理器
        this.handleChange = this.handleChange.bind(this)
        this.handleSubmit = this.handleSubmit.bind(this)
    }
    handleChange({target}){
    	this.setState({
        	[target.name]:target.value,
    	})
	}
    handleSubmit(e){
        e.preventDefault()
        console.log(`${this.state.firstName}${this.state.lastName}`)
    }
    //需要重点修改的是渲染方法
    render(){
        return(
            <form onSubmit={this.handleSubmit}>
        		<input 
                    type="text" 
                    name="firstName"
                    value={this.state.firstName}
                    onChange={this.handleChange} 
                />
                <input 
                    type="text" 
                    name="lastName"
                    value={this.state.lastName}
                    onChange={this.handleChange} 
                />
        		<button>Submit</button>
    		</form>
        )
    }
    
}
```

首次渲染表单时，React将状态中的初始值作为输入框的值，当用户输入一些内容后，handleChange函数被调用，并将输入框的新值保存进状态。当状态发生变化时，React会重新渲染组件，并在次将状态值显示为输入框的当前值。

现在我们完全掌控了表单元素的值，这种模式称为受控组件。

###  JSON schema

接下来学习表单的自动创建，最流行的解决方案就是由mozilla-services所维护的react-json-schema-form。

首先，用npm安装这个库`npm install --save react-jsonschema-form`

安装完成后，在组件内导入这个库

```react
import Form from 'react-jsonschema-form'
//然后定义如下所示的schema
const schema = {
    type:'object',
    properties:{
        firstName:{type:'string', default:'Dan'},
        lastName:{type:'string', default:'Abramov'},
    },
}
```

如上所示，我们将schema的类型设为对象，然后声明表单的firstName和lastName属性，每个属性都有各自的字符串类型与默认值。将schema对象传递给从库中导入的Form组件，就会自动生成一张表单。

```react
const JSONSchemaForm = () => (
    <Form schema={schema} />
)
```

现在我们希望在提交表单时收到通知，并对表单数据进行某些处理

```react
class JSONSchemaForm extends React.Component{
    constructor(props){
        super(props)
        
        this.handleSubmit = this.handleSubmit.bind(this)
    }
    //handleSubmit处理器将收到一个对象，该对象的formData属性包含了表单域的名称和值
    handleSubmit({formData}){
        console.log(formData)
    }
    //需要重点修改的是渲染方法
    render(){
        return(
            <Form schema={schema} onSubmit={this.handleSubmit} />
        )
    }
    
}
```



##  事件

