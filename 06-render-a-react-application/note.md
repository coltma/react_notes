## 05-render-a-component-conditionally
2018-1-3

React will preserve element focus and only do the minimal required DOM operations for the re-render.
>Whenever you re-render on the same element or whenever React is doing a re-rendering, it is only going to be updating the part of the DOM that's necessary for it to re-render.

1. Only render the changing part, not losing focus. (Chrome, Inspect)
```html
<div id="root"></div>
<script src="https://unpkg.com/react@16.0.0-rc.3/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16.0.0-rc.3/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/babel-standalone@6.26.0/babel.js"></script>
<script type="text/babel">
const rootElement = document.getElementById('root')
function tick(){
    const time = new Date().toLocalTimeString()
    const element = <div>It is {time}</div>
    const element1 = <div>It is <input value={time} /></div> //not losing focus
    ReactDOM.render(element, rootElement)
}
tick()
setInterval(tick, 1000)
</script>
```
2. Change from `JSX` to a `template string` and update the entire DOM structure.
```JavaScript
//Template String to be interpolated:
 `<div> "${time}" </div>`
```
```javascript
function tick(){
    const time = new Date().toLocalTimeString()
    const element = `
        <div>
            It is
            <input value="${time}" />
            <input value="${time}" />
        </div>
    `
    rootElement.innerHTML = element //update the entire DOM structure
    // ReactDOM.render(element, rootElement)
}
```
