## 05-render-a-component-conditionally
2018-1-1

1. Using `if` and JSX.
  ```javascript
  function Message({message}) {
      if (!message) {
          return<div>No Message</div>
      }
      return<div>{message}</div>
  }

  ReactDOM.render(
      <Message message="hi there" />,
      document.getElementById('root'),
  )

  ReactDOM.render(
      <Message message={null} />,
      document.getElementById('root'),
  )
  ```

2. Using `if` and raw JavaScript.
  ```javascript
  function Message({message}) {
    if (!message) {
        return React.createElement('div', null, 'No Message')
    }
    return React.createElement('div', null, message)
}
  ```

3. Ternary
  ```javascript
  function Message({message}) {
      return message
          ? React.createElement('div', null, message)
          : React.createElement(
              'div',
              null,
              'No Message'
          )
  }
  ```

4. Wrap all of our return inside of another `<div>` and raw JavaScript
  ```javascript
  function Message({message}) {
    return (
        <div>
            {message
                ? React.createElement(
                    'div',
                    null,
                    message
                )
                : React.createElement(
                    'div',
                    null,
                    'No Message'
                )
            }
        </div>
    )
  }
  /**
   * Why ternaries?
   * because an if statement doesn't work in there
   * <div>{...}</div>.
   *
   * Using ternaries to conditionally render different
   * components is a really nice way to compose these
   * components together.     
   */
  ```

5. Ternary with JSX

  ```javascript
  function Message({message}) {
      return (
          <div>
              {message ? (
                  <div>{message}</div>
              ) : (
                  <div>No Message</div>
              )}
          </div>
      )
  }

  ReactDOM.redner(
      <Message message={null} />
      document.getElementById('root'),
  )
  ```
