## 02-JSX-React
2017-12-05

1.JSX element & babel

babel transpiles into React.createElement call

```javascript
<script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>

<script type="text/babel">
const element = <div/> //JSX element
ReactDOM.render(element, rootElement);
</script>
```
---
2.className & interpolation

```javascript
<script type="text/babel">
const element = <div className={ any JavaScript }/>
ReactDOM.render(element, rootElement);
</script>
```
---
3.props object

Remove all the props of the "div" and make it a self-closing React element.
```javascript
const props = {
    className: 'row',
    children: 'Hello World'
}
const element = (
    <div {...props} />
)
```
---
4.override props

have content after the "...props" spread, and it would override whatever's in the ...props there.
```javascript
const props = {
    className: 'row',
    children: 'Hello World'
}
const element = (
    <div {...props} className="newClassName" children="our own Content"/>
)
```
or
```javascript
const element = (
    <div {...props}>our own content</div>
)
```

5.Do a self-closing tag as well if you don't want to put any children inside of the JSX element.
```javascript
const element = (
    <div/> // Self closing.
)
```
