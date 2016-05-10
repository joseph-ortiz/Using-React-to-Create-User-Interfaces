# Using-React-to-Create-User-Interfaces

Existing problem with user interfaces  

##Why React?  
You may be asking yourself why you would want to write a webapp in react if I already know HTML. You may be thinking that writing your view in javascript is ludicrous but as you develop your web app, you will notice that scanning through your HTML can cause a lot of memory management to understand what is going on. For example, a navigation bars, progress bars, jumbotrons can have many classes and semanticaly placed for it to render correctly. React can resolve this by making you write it one time and reuse the component later.

##My first impression of React.js by building a component
So I finally got serious and went through the tutorial on facebook’s page for React.JS. The tutorial walked me through creating a comment component made up of a comment, comment box, and a comment form. I realized, once you write a component, creating another one is very similar.  


I decided to create a component from bootstrap. In this case I have created the Jumbotron component from bootstrap.
[Full Link] (https://gist.github.com/joseph-ortiz/33d841265acd721cb9848af73b610986)
```javascript
class Jumbotron extends React.Component {
  render() {
    return (
      <div className="jumbotron">
        <h1>{this.props.mainText}</h1>
        <p>{this.props.subText}</p>
         <p><a class="btn btn-primary btn-lg" href="#" role="button">Learn more</a></p>
      </div>
    )
  }
}

React.render(<Jumbotron mainText="Hello, world!" subText="this is the subtext"/>, document.getElementById('main'));
```

A React.js component from the surface appears to be a javascript class that extends a React Component. This class object has a minimum of the the render() method. You can even throw ajax in the component.
Components are self describing. I love how you can navigate through the various components and know where you are in the code. If I’m trying to create a Jumobtron component from bootstrap, I go to the Jumbotron component. For me, components made it easier for me to conceptualize and build.

An intersting feature when creating React components is the ability to create your own custom properties. You will notice that in the component, there are curly braces syntax that says: 
```javascript 
{this.props.mainText}
```

This is telling you how the component will be used. Specifically it says that the mainText property on the component will be rendered here. You can see the Jumbotron component use the mainText property by seeing the line below:
```javascript
React.render(<Jumbotron mainText="Hello, world!" subText="this is the subtext"/>, document.getElementById('main'));
```

Another cool feature with React is the composition of components. In the jumbotron example, I decided to extract out the Primary Button that says learn more into it's own component. I create a PrimaryButton component that has a single property for the button text. See below.

```javascript
class PrimaryButton extends React.Component {
  render() {
    return (
      <div>
         <p><a className="btn btn-primary btn-lg" href="#" role="button">{this.props.buttonText}</a></p>
        </div>
    )
  }
}
```

I then go ahead and use that PrimaryButton and place it back into the Jumbotron Component where we originally had the button.
```javascript
class Jumbotron extends React.Component {
  render() {
    return (
      <div className="jumbotron">
        <h1>{this.props.mainText}</h1>
        <p>{this.props.subText}</p>
        <PrimaryButton buttonText='Learn more'/>
      </div>
    )
  }
}

class PrimaryButton extends React.Component {
  render() {
    return (
      <div>
         <p><a className="btn btn-primary btn-lg" href="#" role="button">{this.props.buttonText}</a></p>
        </div>
    )
  }
}

React.render(<Jumbotron mainText="Hello, world!" subText="this is the subtext"/>, document.getElementById('main'));
```


Some reasons why working with React is easier for me is because of the following:
-  When writing React using jsx you will notice that the jsx syntax looks similiar to XML/HTML. 
-  I liked how you can breakdown components into smaller components.
-  I love how you can nest components
-  Properties can be whatever you want.

I followed the tutorial here:https://facebook.github.io/react/docs/tutorial.html

##Thinking in React  
As I delve deeper into React their is a workflow when creating your React app, 
[“Thinking in React”](https://facebook.github.io/react/docs/thinking-in-react.html) helped piece together an approach to creating your app.

If you want an in-depth description check out the link above otherwise you can read my short snippet on my takeaways. Writing these thoughts down have helped me understand React more effectively.

Five steps to follow when you want to “Think in React”  
Step 1: break the UI into a component hierarchy  
— draw or sketch out your UI. then draw boxes around each component. This will define your hierarchy and gives you a game plan.

Step 2: Build a static version in React  
— I’ve learned state can cause headaches,building static makes life easier! Not only will you code faster but you reduce complexity.   Their should only be a render() in each component. Their is NO interactivity yet.  
Key: React flows in one direction and computes everything down the line!  

Step 3: Identify the minimal (but complete) representation of UI state  
1.  Ponder what is the minimum number of states by asking three questions Is it passed in from a parent via props? If so, it probably isn’t state.  
2. Does it change over time? If not, it probably isn’t state.  
3. Can you compute it based on any other state or props in your component? If so, it’s not state.  

Step 4: Identify where your state should live  
— Find every component that handles state, consider using a parent component or making a parent component to hold the state  

Step 5: Add inverse data flow  
— Since components handle their own state, you need to pass a callback to the child component that changes it’s state. In the FB example, they had a parent table that attached a callback to the searchbar. The Searchbar then has an onChange event that reads in the user input to a property. By setting this property, the parent table renders the component again with the correct data.

## Using JSX and learnings
As my journey through the world of React components continue. I’m now reading about JSX, a JavaScript extension that looks simliar to XML. I think that JSX makes components easier to understand by giving you a declarative hierarchy of a component and it’s composition. It’s beautiful. This relationship was an easy concept for me to wrap my ahead around.

A part of learning React that drove me crazy at first was the convention that *lower case letters represent html tags*.  *Components must have start with a capital letter*. When trying to follow along some React tutorials, I lost a lot of time looking line by line trying to figure out what went wrong. Luckily, the documentation rescued me.

JSX is transformed from this javascript/xml like syntax to plain old Javascript. Another cool thing that the docs taught me was the concept of namespacing your components. You can create a component like “MyComponent” and then create another component as a property on that Component using dot notation like “MyComponent.AnotherComponent”.

The similarities of JSX and HTML confused me at first with the way values are expressed.
In HTML land, attributes would be formed in the opening tag like:  
```html
<Dog breed=”Snoop”.>.
```
In React City, attributes are interpolated with curly brackets like:  
```jsx
<Dog breed={Snoop}/>
```
Retrospectively thinking, curly brackets are commonplace in Mustache, AngularJS, Laravel. It is currently one of the coolest way to render expressions on the front-end. Also check out how you can render Child Expressions like displaying a nav or login.
What I Learned:
-  JSX looks like HTML
-  Capital for Component and lower case for HTML
-  Consider Namespacing components in situations with lots of children.
-  Use curly braces instead of double quotes when rendering JSX attributes.


React.js is a beautiful view rendering library with a workflow that helps you build composible and resuable components.

