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

behind the scenes this webpage is using **[JSX]([http://facebook.github.io/jsx/](http://facebook.github.io/jsx))** to compile something that the browser can understand, the [playground](https://jscomplete.com/playground) is using a special compiler named [Babel](https://babeljs.io) to convert `JSX` into `React API Code`, example:

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
3 	return <button onClick={() => setCounter(counter+1)}>{counter}</button>;
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
>
> - `line 7`: is calling to the function `Button()` previosly created
> - `line 8`: where the document will be **rendered**