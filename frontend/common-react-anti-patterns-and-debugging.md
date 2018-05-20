# Common React Anti Patterns and Debugging

This read is highly recommended if you are just beginning to work with React. Many common problems arise to all developers working with this new paradigm of UI development. I've also included different ways of writing code syntatically in the examples in React

### 1. use `setState()`

Use `this.setState()` to change state. It triggers a re-render. `this.state.someValue = value`does not trigger a re-render.

### 2. `setState()` is asynchrounous

> setState\(\) does not always immediately update the component. It may batch or defer the update until later. This makes reading this.state right after calling setState\(\) a potential pitfall. - [Official docs](https://reactjs.org/docs/react-component.html#setstate)

For example, MyComponent takes in prop `increment`, which defines how much is incremented when the button is pressed.

```javascript
class MyComponent extends React.Component {
    state = {
        number: 0
    }
    // BAD
    increment = e => {
        this.setState({
            number: this.state.number + this.props.increment
        })
    }

    // GOOD
    increment = e => {
        this.setState((prevState, props) => ({
            number: prevState.number + props.increment
        }))
    }

    render(){
        return(
            <button onClick={ this.increment }>{ this.state.number }</button>
        )
    }
}
```

Say we used the bad version and `this.props.increment` was 1 and `this.state.number` was 0. If we clicked the button, the state would be `1` because the state was `0` previously. If we quickly press it again, we would think that the number would be changed to 2 because the button was pressed twice and the "previous" state was 1. However, this may not happen because of the asyncrhonity of `setState`. The second call may still see that the state is still 0. Thus, use the second version whenever your next state is dependent on the previous state.

### 3. `.bind` vs Arrow Functions

Arrow functions auto bind :\) One of the first things that may happen is using the `.bind` operator on class functions that handle events from HTML elements such as buttons or input forms. This is because the compiler, Babel, will return an error message yelling at you to `bind` this certain function. You may end up with something like this:

```javascript
class MyComponent extends React.Component {
    constructor(props){
        super(props)
    }
    handleClick(event) {
        console.log("button was clicked")
    }
    render() {
        return(
            <button onClick={this.handleClick.bind()}>Click Me!</button>
        )
    }
}
```

This works and compiles! However, the function `handleClick()` is binded to the class everytime the state changes and the Component is re-rendered, which happens quite a bit. To fix it you may do inside the constructor:

```text
this.handleClick = this.handleClick.bind(this)
```

However, why not remove that line and instead use Arrow functions.

```javascript
class MyComponent extends React.Component {
    handleClick = (event) => {
        console.log("button was clicked")
    }
    render() {
        return(
            <button onClick={ this.handleClick }>Click Me!</button>
        )
    }
}
```

### 4. Props vs State

As a rule of thumb, if a certain prop that you pass into a Component **does not** change inside that Component, directly access props and do not set a state attribute equal to that prop.

```javascript
// BAD
class TextBoxComponent extends React.Component{
    constructor(props){
        this.state = {
            text: this.props.text
        }
    }
    render() {
        return (
            <div>
                <p>{ this.state.text }</p>
            </div>
        )
    }
}

// GOOD 
class TextBoxComponent extends React.Component{
    render(){
        return (
            <div>
                <p>{ this.props.text }</p>
            </div>
        )
    }
}
```

#### Explanation

For example, say we have a Parent Component that passes a prop to a text box Component that will display that prop value.

```javascript
class ParentComponent extends React.Component {
    render() {
        return(
            <TextBoxComponent text="Hi, I'm text"/>
        )
    }
}
```

Now, to write the `TextBoxComponent`, one may decide to set `this.state.text` equal to `this.props.text` and then access `this.state.text` in `render`

```javascript
class TextBoxComponent extends React.Component{
    constructor(props){
        this.state = {
            text: this.props.text
        }
    }
    render() {
        return (
            <div>
                <p>{ this.state.text }</p>
            </div>
        )
    }
}
```

However, the state is useless in this scenario because there is no other logic in changing the displayed text inside `TextBoxComponent`. Thus, instead, in the render function, you can directly access the props like this:

```javascript
render(){
    return (
        <div>
            <p>{ this.props.text }</p>
        </div>
    )
}
```

### 5. Initial State and Props

This stems off of \#4, so please read that first. Given the previous example in \#4, if `ParentComponent` has additional logic that changes the value of the prop passed into `TextBoxComponent`, we will see that the text doesn't change. Let's step through this. Say `ParentComponent` has an array of words where one of the words will be randomly picked everytime a button is pressed.

```javascript
class ParentComponent extends React.Component {
    constructor(props){
        super(props)
        this.words = ['bananas1', 'bananas2', 'bananas3', 'bananas4']
        this.state = {
            textPassedIn: this.words[0]
        }
    }
    changeText = e => {
        this.setState({
            textPassedIn: this.words[Math.floor(Math.random() * this.words.length)]
        })
    }
    render() {
        return(
            <div>
                <TextBoxComponent text={ this.state.textPassedIn }/>
                <button onClick={ this.changeText }>Random Word!</button>
            </div>
        )
    }
}
```

If you took the same `TextBoxComponent` using the initial state:

```javascript
class TextBoxComponent extends React.Component{
    constructor(props){
        this.state = {
            text: this.props.text
        }
    }
    render() {
        return (
            <div>
                <p>{ this.state.text }</p>
            </div>
        )
    }
}
```

If you pressed the button, in `ParentComponent`, the text will not change, no matter what \( assuming that the random text has changed \). This is because the state does not change when new props are passed. Thus, `TextBoxComponent` isn't re-rendered and `this.state.text` is still the same as it was initially. To fix this, you must add the class function `componentWillRecieveProps`:

```javascript
class TextBoxComponent extends React.Component{
    constructor(props){
        super(props)
        this.state = {
            text: this.props.text
        }
    }
    componentWillReceiveProps(nextProps) {
        if (nextProps.text !== this.state.text){
            this.setState({
                text: nextProps.text
            })
            // Fun fact: this can also look like this
            // this.setState({ ...nextProps })
            // ... is called Spread Operator
        }
    }
    render() {
        return (
            <div>
                <p>{ this.state.text }</p>
            </div>
        )
    }
}
```

Of course, this wouldn't make sense if there isn't logic that may change the text inside `TextBoxComponent` and you would accomplish the same thing with directly accessing the props shown in \#4. Now, if you have a button that's changing the text inside the `<p>` tags, then you would use the state because there is additional logic in `TextBoxComponent`. Note that `ComponentWillRecieveProps` and a couple more lifecycle functions will be deprecated in React 17, which will require the use of another [new function](https://reactjs.org/blog/2018/03/27/update-on-async-rendering.html). For now, don't worry about it.

```javascript
class TextBoxComponent extends React.Component{
    state = {
        text: this.props.text
    }
    handleClick = (event) => {
        this.setState((prevState, props) => ({
            text: prevState + "1"
        }))
    }
    render() {
        return (
            <div>
                <p>{ this.state.text }</p>
                <button onClick={this.handleClick}>Click Me!</button>
            </div>
        )
    }
}
```

Note that you could don't need to use the constructor to intialize `this.state`.

#### Debugging

Much of debugging react is dealing with Components not re-rendering. If something is not changing when it's supposed to, or it's not rendering, check your state and how you change it. Is your element using props instead of the state? Are you correctly doing everything that was mentioned above? Try to print out your states for every render or use the React Chrome Extension dev tools.

