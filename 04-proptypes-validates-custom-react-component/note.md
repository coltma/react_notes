## 04-proptypes-validates-custom-react-component
2017-12-19

>Sometimes, we pass wrong type for a props' property
```javascript
  function Hello(props) {
    return (
      <div>
        Hello {props.name} {props.department}
      </div>
    )
  }
  ReactDOM.render(
    <Hello name={true} />,
    document.getElementById('root')
  )
  // wrong type for props.name and missing props.department!
```

1. Define a `propTypes` object for a function component like `Hello`
```javascript
// validates key 'name' as a function.
Hello.propTypes = {
  name(props, propName, componentName) }
     if (typeof this.props[propName] !== 'string') {
       return new Error(`You should pass a string for
         ${propName} in ${componentName}, but you pass a
         ${typeof props[propName]}`)
     }
}
// console will show error msg.
```

2. Hold the validation function out as an object
```javascript
// improve code quality
// string as a property of PropTypes
const PropTypes = {
  string(props, propName, componentName) {
    if (typeof this.props[propName] !== 'string') {
      return new Error(`You should pass a string for
          ${propName} in ${componentName}, but you pass a
          ${typeof props[propName]}`)
    }
  }
}
// states propTypes
Hello.propTypes = {
  name: PropTypes.string,
  department: PropTypes.string,
}
// console will show error msg.
```

3. Using official PropTypes solution instead
  ```javascript
  // Add a global PropTypes for our program
  <script src="https://unpkg.com/prop-types@15.6.0/prop-types.js"></script>
  function Hello(props) {
    return (
      <div>
        Hello {props.name} {props.department}!
      </div>
    )
  }

  Hello.propTypes = {
    name: PropTypes.string,
    department: PropTypes.string,
  }

  ReactDOM.render(
    <Hello name={true} />,
    document.getElementById('root')
  )
  /*
   * Console only states {name} type error, no error for    * missing {department}, because every property's
   * PropTypes is
   * optional.
   */
  ```

4. Default value for prop and required prop
  ```javascript
  // Default value
  function Hello(props) {
    return (
      <div>
        Hello {props.name}
        {props.department || 'Default Value Here'}!
      </div>
    )
  }

  // Required prop
  Hello.propTypes = {
    name: PropTypes.string.isRequired,
    department: PropTypes.string,
  }
  ```

5. Using class component instead of function component
  ```javascript
  class Hello extends React.Component {
    static propTypes = {
      name: PropTypes.string.isRequired,
      department: PropTypes.string.isRequired,
    }
    render() {
      const {name, department} = this.props
      return (
        <div>
          Hello {name} {department}
        </div>
      )
    }
  }
  /**
   * This is allowed to do so, but a more common way is to state
   * it as a static property inside the component class
   */
  Hello.propTypes = {
    name: PropTypes.string.isRequired,
    department: PropTypes.string.isRequired,
  }
  ```

6. Proptypes validation difference in React development version VS production version

  PropTypes slows things down so it is not necessary in production. React remove PropTypes in production.

  Using `babel-plugin-transform-react-remove-prop-types` will automatically remove `PropTypes` when build production.
  ```javascript
  <script src="https://unpkg.com/react@16.0.0/umd/react.development.js"></script>
  <script src="https://unpkg.com/react-dom@16.0.0/umd/react-dom.development.js"></script>
  //----
  <script src="https://unpkg.com/react@16.0.0/umd/react.production.min.js"></script>
  <script src="https://unpkg.com/react-dom@16.0.0/umd/react-dom.production.min.js"></script>
  ```

### Review
Adding PropTypes Validation
1. Add `.propTypes` property to your component function;
   Or `static propTypes = {...}` to your class component;
2. Keys of your object mapped to your object `props`;
3. Provide function to validate them;
  ```javascript
  function Hello(props) {
    return (
      <div>
        Hello {props.name} {props.department}!
      </div>
    )
  }

  Hello.propTypes = {
    name: PropTypes.string,
    department: PropTypes.string,
  }
  // ---
  class Hello extends React.Component {
    static propTypes = {
      name: PropTypes.string.isRequired,
      department: PropTypes.string.isRequired,
    }
    render() {
      const {name, department} = this.props
      return (
        <div>
          Hello {name} {department}
        </div>
      )
    }
  }
  ```

> Learn from `prop-types` document.
