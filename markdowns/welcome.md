# React Lifecycle Methods: render and componentDidMount

If we are talking about lifecycle methods in React.js then <b>render()</b> is the most used method. If React component has to display any data then it uses JSX. React uses JSX for templating instead of regular JavaScript.

# render() method

As I have talked earlier, <b>render()</b> is the most used method for any React powered component which returns a JSX with backend data. It is seen as a normal function but <b>render()</b> function has to return something whether it is null.  When the component file is called it calls the <b>render()</b> method by default because that component needs to display the HTML markup or we can say JSX syntax.

```javascript
import React, { Component } from 'react';


class App extends Component {
  render() {
    return (
      <div>
          <h1 className="App-title">Welcome to React</h1>
      </div>
    );
  }
}

export default App;
```
Please take a note here; we must return something, if there is no <b>JSX</b> for the return then null would be perfect, but must return something. In that scenario, you can do something like this.

```javascript
import { Component } from 'react';


class App extends Component {
  render() {
    return null;
  }
}

export default App;
```

<b>Remember, you can not define <b>setState()</b> inside <b>render()</b> function. Why???</b>
Because <b>setState()</b> function changes the state of the application and causing a change in the state called the <b>render()</b> function again. So if you write something like this then calling the function stack will go for infinity and application gets the crash.

You can define some variables, perform some operation inside <b>render()</b> function, but never use the setState function. In general cases, We are logging out some variable’s output in the <b>render()</b> method. It is the function that calls in mounting lifecycle methods.

# componentDidMount() method

As the name suggests, after all the elements of the page is rendered correctly, this method is called. After the markup is set on the page, this technique called by React itself to either fetch the data from An External API or perform some unique operations which need the <b>JSX</b> elements.

<b>componentDidMount()</b> method is the perfect place, where we can call the <b>setState()</b> method to change the state of our application and <b>render()</b> the updated data loaded JSX. For example, we are going to fetch any data from an API then API call should be placed in this lifecycle method, and then we get the response, we can call the <b>setState()</b> method and render the element with updated data.

```javascript
import React, { Component } from 'react';

class App extends Component {

  constructor(props){
    super(props);
    this.state = {
      data: 'Jordan Belfort'
    }
  }

  getData(){
    setTimeout(() => {
      console.log('Our data is fetched');
      this.setState({
        data: 'Hello WallStreet'
      })
    }, 1000)
  }

  componentDidMount(){
    this.getData();
  }

  render() {
    return(
      <div>
      {this.state.data}
    </div>
    )
  }
}

export default App;
```

If you see an above example, then I have simulated an API call with setTimeOut function and fetch the data. So, after the component is rendered correctly, <b>componentDidMount()</b> function is called and that call <b>getData()</b> function.

# componentWillMount() method

<b>componentWillMount()</b> method is the least used lifecycle method and called before any HTML element is rendered. If you want to see then check out the example mentioned above, we just need to add one more method.

```javascript
import React, { Component } from 'react';

class App extends Component {

  constructor(props){
    super(props);
    this.state = {
      data: 'Jordan Belfort'
    }
  }
  componentWillMount(){
    console.log('First this called');
  }

  getData(){
    setTimeout(() => {
      console.log('Our data is fetched');
      this.setState({
        data: 'Hello WallStreet'
      })
    }, 1000)
  }

  componentDidMount(){
    this.getData();
  }

  render() {
    return(
      <div>
      {this.state.data}
    </div>
    )
  }
}

export default App;
```

If you will see carefully in the console panel, then it first logs “First this called” and then our initial state is defined and then <b>render()</b> method is called then <b>componentDidMount()</b> method is called and then newly fetched data is displayed in the component.

## Order of the methods till now.

1. componentWillMount()
2. set the initial state in the constructor
3. render()
4. componentDidMount()
5. setState()
6. render()

Following example is the use case of <b>componentDidMount()</b>. In above order, excecutions are done. After 1 second, the state will change and updated state will display.

Initial state is "Jordan Belfort" but after 1 second it will change it to "Hello WallStreet".

# Hands-on Demo

@[Sample React App Boilerplate]({"stubs": ["src/app/app.jsx", "src/main.js"], "command": "./run.sh"})