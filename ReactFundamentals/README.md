# React

React was created and is maintened by Facebook, the formal definition is: **a JavaScript library for building user interfaces**

## The Basics

### React Commonly Faced Problems

:hand: [here](https://jscomplete.com/learn/react-beyond-basics/react-cfp)

### React's Basic Concepts

1. Components
   1. Like functions
   2. Input: props, state | Output: UI
   3. Reusable and composable
   4. <Component/>
   5. Can manage a private state
2. Reactive updates
   1. React will react
   2. Take updates to the browser
3. Virtual views in memory
   1. Generate HTML using JavaScript
   2. No HTML template language
   3. Tree reconciliation

### `jscomplete.com/playground`

The webpage [jscomplete.com/playground](https://jscomplete.com/playground) we will use to write our React code without setup anything<br>

An example of code will be:

```react
function Hello() {
	return <div>Hello React!</div>; // this is not HTML language
}

ReactDOM.render(
  <Hello />, 
  document.getElementById('mountNode'),
);
```

:notebook: ​Behind the scenes this webpage is using **[JSX]([http://facebook.github.io/jsx/](http://facebook.github.io/jsx))** to compile something that the browser can understand, the [playground](https://jscomplete.com/playground) is using a special compiler named [Babel](https://babeljs.io) to convert `JSX` into `React API Code`, example:

1. The following code in `JSX` language:

   ```jsx
   <div>Hello React!</div>
   ```

2. Is converted to `React` code through `Babel` compiler

   ```react
   React.createElement("div", null, "Hello React!");
   ```

   1. `null`: refers to the attributes that the `div` can has

### My First Reac Hook

Official documentation [here](https://reactjs.org/docs/hooks-intro.html)<br>

*An example is*:

```react
1 function Button() {
2  const [counter, setCounter] = useState(0);
3 	return <button onClick={() => setCounter(counter+1)}>{counter}</button>);
4 }
5 
6 ReactDOM.render(
7   <Button />, 
8   document.getElementById('mountNode'),
9 );
```

> - `line 2`: destructuring arrays (unpacking elements into variables)
>   - `userState()`: is a **Hook** and *React* will preserve this state between re-renders. `useState` returns a pair: the *current* state value and a function that lets you update it. You can call this function from an event handler or somewhere else. It’s similar to `this.setState` in a class, except it doesn’t merge the old and new state together, more info [here](https://reactjs.org/docs/hooks-overview.html)
> - `line 3`: event handler was intruduced with an `arrow function`
>- `line 7`: is calling to the function `Button()` previosly created
> - `line 8`: where the document will be **rendered**

### Your First One-way Data Flow

```react
function Button(props){
  // child
  return (
    <button onClick={props.onClickFunction}>
      +1
    </button>
  );
}

function Display(props){
  // child
  return (
    <div>{props.message}</div>
  );
}

function App (){
  // parent
  const [counter, setCounter] = useState(42);
  const incrementCounter = () => setCounter(counter+1);
  return (
    <div>
      <Button onClickFunction={incrementCounter}/>
      <Display message={counter}/>
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('mountNode'),
);
```

This is a very good example to separate responsabilities and make readable the code

- `function Button()`: 
  - This function is a child from a parent called `App()`
  - The variable `props` (can renamed to whatever you want) is a convention for *properties* that could contains several values in a relationship of *keys-values* that can be access like `props.<propertyName>`
- `function Display()`:
  - This function is also a child from `App()` (for the simple reason that is being calling from there)
- `function App()`:
  - This function is a parent function for the mentioned ones simply because this calls to them
  - `userState()`: is a [hook](https://reactjs.org/docs/hooks-overview.html)
  - `incrementCounter`: this variable increment the counter every time that the user click on the button
  - `return()`: to call several functions (multiple elements) in **ReactDOM.render()** is needed a *<div>* thus this tag would be the parent from the functions inside, you can use: `<React.Fragment></React.Fragment>`/`<></>` in order to dont introduce a parents for the multiples elements on it
  - `<Button>`: this function can have several propierties on it, and those can name as the user wants, to introduce more than one propierties is enought to separate them with an empty space

### Components Reusability

```react
function Button(props){
  // child
  const handleClick = () => props.onClickFunction(props.increment);
  return (
    <button onClick={handleClick}>
      +{props.increment}
    </button>
  );
}

function Display(props){
  // child
  return (
    <div>{props.message}</div>
  );
}

function App (){
  // parent
  const [counter, setCounter] = useState(0);
  const incrementCounter = (incrementValue) => setCounter(counter+incrementValue);
  return (
    <div>
      <Button onClickFunction={incrementCounter} increment={1} />
      <Button onClickFunction={incrementCounter} increment={5}/>
      <Button onClickFunction={incrementCounter} increment={10}/>
      <Button onClickFunction={incrementCounter} increment={100}/>
      <Display message={counter}/>
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('mountNode'),
);
```

The above code reuses the **component Button**, there will be 4 buttons

### Tree Reconcilliation in Action

```react
const render = () => {
  // JavaScript Code
  document.getElementById('mountNode').innerHTML = `
    <div>
      Hello HTML
      <input/>
        <pre>${(new Date).toLocaleTimeString()}</pre>
    </div>
    `;
  
  // React Code
  ReactDOM.render(
    React.createElement(
    "div", "null", "Hello React",
    React.createElement('input', null),
    React.createElement('pre', 'null', (new Date).toLocaleTimeString()),
    ),
    document.getElementById('mountNode2'),
  );
}

setInterval(render, 1000);
```

This example show us the differences between `JavaScript` & `React`

- `JavaScript`: the code renders texts and a `input` to write on it, but this code by default re-writes all the DOM every 1 second due to **setInverval()** function
- `React`: the code renders the same as the `JavaScript` code except that **React** only render every second the tag `pre` allowing us to write in the `input` field