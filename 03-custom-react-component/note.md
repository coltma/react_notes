## 03-Custom-React-Component
2017-12-08

To create reusable components

1.`React.createElement()` takes a string or function

```javascript
// Take function:
const message = () => <div>{props.msg}</div>

const element = (
  //JSX compiles down to React.createElement call
  <div>{React.createElement(message({msg: 'Hello'}))}</div>
  <div>{React.createElement(message({msg: 'Bye bye'}))}</div>
)

// Take string:
const element = React.createElement('div', {
  className: 'container',
  children: 'Hello World'
})
```
---
2.Switch `React.createElement` with a quotes `<div>` to JSX `<div>`
```javascript
const message = () => <div>{props.msg}</div>
const element = (
  <div>
    <message />  
  </div>
)

// <message></message> can be rendered in HTML, babel transpiles JSX
// statement into React.createElement("message", null), reference
// message variable as a string.
```
JSX to differentiate a variable that's in `scope` or a `raw DOM element`, need to capitalize your component `Message`.

```javascript
const Message = props => <div>{props.msg}</div>
const element = (
    <div className="container">
        <Message msg='Hello World' />
        <Message msg='Goodbye World' />
    </div>
)
```
---
3.`children prop`

```javascript
const element = (
    <div className="container">
        <Message>
            Hello World
                <Message>Goodbye World</Message>
        </Message>
    </div>
)
```
