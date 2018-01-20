## 07-style-react-component
2018-1-5

> Style react component using `style` prop and `className` prop. Values are not vendor prefixed for you when use `style` prop, so you have to do that yourself.

> In-line styles problems please check libraries: `styled components`, `emotion` and `glamorous`.

1. Style: HTML->string; JSX->object; And the object property keys are camel-cased (not as cabob-cased in CSS), values are strings.
```javascript
const element = (
    <div>
        <div style={{paddingLeft: '20px'}}>box</div>
    </div>
)
```
If value is pixels, we can change it to a number instead of a string. React will treat that as a pixel value.
```javascript
const element = (
    <div>
        <div style={{paddingLeft: 20}}>box</div>
    </div>
)
```

2. Object Shorthand
```javascript
// extract the className value into a variable called
// className and use object shorthand to add it to the props.
const className = 'box box--small'
const props = {
    className,
    style: {paddingLeft: 20},
}
```

3. Object spread does a shallow merge of the objects given
```javascript
function Box(props){
    return (
        <div
            className="box box--small"
            style={{paddingLeft: 20}}
            {...props}
        />
    )
}
const element = (
    <div>
        <Box style={{backgroundColor: 'lightblue'}}>
        small box
        </Box>
    </div>
)
/**
 * We will lost style "paddingLeft: 20" with only
 * "backgroundColor: 'lightblue'" instead.
 * Because object spread does a shallow merge of the
 * objects given, so the style prop given to the Box
 * component is overriding its own style prop.
 */
```
Merge the style prop with our own style:

  ```javascript
  /**
   * Destructure the props, pull out the style prop, and
   * call the rest of the props rest.
   * spread the ...rest props onto the <div>
   */
  function Box({style, ...rest}){
    return (
        <div
            className="box box--small"
            // merge our own style with style prop.
            style={{paddingLeft: 20, ...style}}
            {...rest}
        />
    )
  }
  ```
