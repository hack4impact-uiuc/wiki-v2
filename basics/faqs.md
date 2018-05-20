# FAQs

### My form isn't making an HTTP API request when it's submitted?

By default, the form tries to submit itself by calling the URL you are at and having the form inputs as the parameters. You need to prevent this default action by using \`event.preventDefault\(\)\`

```javascript
class MyComponent extends React.Component {
    submitForm = e => {
         e.preventDefault()
         // handle submission    
    }
    render {
         return( 
             <form onSubmit={this.submitForm}>
                  <div>
                        <label htmlFor="name_input">Lesson Worksheet: </label>
                        <input id="name_input" name="name" value={this.state.name} onChange={this.handleChange} />
                  </div>         
             </form> 
        )
    }
}
```

### How do I pass in an argument into a called function in JSX?

In general, be careful when you would want to do this. You should usually use \`props\` and \`this.state\` as much as you can before you need to pass in an argument in JSX. There shouldn't be many instances where you would need to do this. But if you need to, you must remember the event object in u need to use it. Below, \`e\` is the event object created whenever the button is clicked. 

```javascript
class MyComponent extends React.Components {
     submit = (e, parameter) =>{
         e.preventDefault()
         // do whatever you want
     }
     render() {
          return(
              <button onClick={e => submit(e, parameter)}>Submit</button>
          )
     }
}
```



