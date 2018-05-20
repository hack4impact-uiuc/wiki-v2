# React

React is a very popular library for creating user interfaces. React is component-based and declarative and it allows you to compose an interface built up with a bunch of small components, with each component having its own functionality and all the HTML/CSS/JS. The Component-based architecture is like writing a regular program that is built up of a bunch of functions, but instead, you’re applying this to components, where you have multiple small components that build up the UI. This allows you to encapsulate complexity into components, and then bring these components together to build the overall interface.

As an example, we create a Component called Demo, where it renders a `h1` and an `OtherComponent` component.

```javascript
import OtherComponent from './'
export default class Demo extends Component {
  state = {
    year: 2018
  }
  render() {
    return (
      <div>
        <h1>Hello World!</h1>
        <div>
          <OtherComponent year={this.state.year} />
          <p>Current Year: {this.state.year}</p>  
        </div>
      </div>
    )
  }
}
```

#### Why React

Many of the applications we will be building will utilize React. This is because:

* Working with and manipulating the DOM is hard, especially for more complicated applications.
* React is Javascript and has a very small API, allowing one to pick up very fast
* React is **declarative**, meaning we describe User Interfaces with React and tell it what we want \(not how to do it\)
* You can use reusable, composable, and stateful components in React

Along with awesome, immutable state management in redux with React router to provide it with multiple pages, React is a powerful tool that we trust for building the Frontend for many of our applications.

We generally will use vanilla React with create-react-app. However, it has a huge learning curve for beginners, having to learn client-side routing, page layout, Single Page applications, etc. We are currently trying to figure out the best way to teach this since many applications will require the use of Redux, React Router, and Flow \(type checking since `propTypes` have been deprecated\), which is a ton of stuff to learn in a short timespan we give you.

### Explore More

* [Official Docs & Tutorial](https://reactjs.org/docs/hello-world.html)
* [Egghead Tutorial](https://egghead.io/courses/the-beginner-s-guide-to-reactjs)
* [create-react-app](https://github.com/facebook/create-react-app) - boilerplate code we usually build up from
* [I wish I knew these before diving into React](https://engineering.opsgenie.com/i-wish-i-knew-these-before-diving-into-react-301e0ee2e488)
* [Clean Code vs Bad Code: React Components](http://americanexpress.io/clean-code-dirty-code/)
* [How to structure React Components](https://reallifeprogramming.com/how-to-structure-components-in-react-54fc43e71546)
* [8 Things to learn before learning Redux](https://www.robinwieruch.de/learn-react-before-using-redux/)
* [React State & Redux State](https://spin.atomicobject.com/2017/06/07/react-state-vs-redux-state/)
* [Compilation of React Patterns and Tips](https://vasanthk.gitbooks.io/react-bits/)
* [Handling States in React](https://medium.freecodecamp.org/handling-state-in-react-four-immutable-approaches-to-consider-d1f5c00249d5)

