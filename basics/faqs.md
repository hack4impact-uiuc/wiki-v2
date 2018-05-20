# FAQs

\#\# My form isn't making an HTTP API request when it's submitted?

By default, the form tries to submit itself by calling the URL you are at and having the form inputs as the parameters. You need to prevent this default action by using \`event.preventDefault\(\)\`

\`\`\`Javascript

class MyComponent extends React.Component {



    submitForm = e =&gt; {

         e.preventDefault\(\)

         // handle submission    

    }

    render {

         render\(\) {

             &lt;form onSubmit={this.submitForm}&gt;

                  &lt;div&gt;

                        &lt;label htmlFor="name\_input"&gt;Lesson Worksheet: &lt;/label&gt;

                        &lt;input id="name\_input" name="name" value={this.state.name} onChange={this.handleChange} /&gt;

                  &lt;/div&gt;         

             &lt;/form&gt; 

    }

}

\`\`\`

\#\# How do I pass in an argument into a called function in JSX?

In general, be careful when you would want to do this. You should usually use \`props\` and \`this.state\` as much as you can before you need to pass in an argument in JSX. There shouldn't be many instances where you would need to do this. But if you need to, you must remember the event object in u need to use it. Below, \`e\` is the event object created whenever the button is clicked. 

\`\`\` Javascript

class MyComponent extends React.Components {

     submit = \(e, parameter\) =&gt;{

         e.preventDefault\(\)

         // do whatever you want

     }

     render\(\) {

          return\(

              &lt;button onClick={e =&gt; submit\(e, parameter\)}&gt;Submit&lt;/button&gt;

          \)

     }

}

