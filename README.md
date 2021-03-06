## Flashcard: a React,Express,Sqlite app

![splash](https://user-images.githubusercontent.com/18589970/59184020-0fb24100-8b22-11e9-870c-c07379973462.png)

![START](https://user-images.githubusercontent.com/18589970/59184022-0fb24100-8b22-11e9-8932-20d90acb26ca.png)

![ANSWER](https://user-images.githubusercontent.com/18589970/59184015-0fb24100-8b22-11e9-9073-d0f0878fefe3.png)

![correctA](https://user-images.githubusercontent.com/18589970/59184018-0fb24100-8b22-11e9-90fd-eaa9f15d6ada.png)

- server.js : express server and sqlite database
- public/index.html: entry point
- src/main.js: entry point for React code defined in webpack.config.js.
  > The entry point is the file webpack looks for to start building your Javascript bundle.

## Usage

1. Get [Cloud Translation API from Google](www.console.developers.google.com/apis) client ID and secret, fill in  line 17-18 in `server.js`

``
const GOOGLE_CLIENT_ID = '' ``

``
const CLIENT_SECRET = ''
``

2. npm install

3. `node server.js`

4. Open [http://localhost:5000](http://localhost:5000).

Credit:

1.https://github.com/ahfarmer/minimal-react-starter



## Cool React Patterns

### [Destructuring React props for the cleaner code](https://dev.to/arnas/destructuring-react-props-for-the-cleaner-code-293)

- Class Component

```
import React from "react";

class Row extends React.Component {
  state = {
    showEmail: false
  };

  render() {
    const { firstName, lastName, email, doSomethingAmazing } = this.props;
    return (
      <div>
        <div>
          <span>First Name: {firstName}</span>
        </div>
        <div>
          <span>Last Name: {lastName}</span>
        </div>
        {this.state.showEmail && (
          <div>
            <span>Email: {email}</span>
          </div>
        )}
        <button onClick={doSomethingAmazing}>Click me</button>
      </div>
    );
  }
}
```

- Functional Component

```
import React from "react";

const Row = ({ firstName, lastName, email, doSomethingAmazing }) => (
  <div>
    <div>
      <span>First Name: {firstName}</span>
    </div>
    <div>
      <span>Last Name: {lastName}</span>
    </div>
    <div>
      <span>Email: {email}</span>
    </div>
    <button onClick={doSomethingAmazing}>Click me</button>
  </div>
);
```

### [React setState usage and gotchas](https://itnext.io/react-setstate-usage-and-gotchas-ac10b4e03d60)

- Basic pattern

```
this.setState({quantity: 2})
```

- Due to the async nature of setState, it is not advisable to use this.state to
  get the previous state within setState. Instead, always rely on the prevState
  and props. Both prevState and props received by the updater function are
  guaranteed to be up-to-date. The output of the updater is shallowly merged
  with prevState.

```
this.setState((prevState) => {
  return {counter: prevState.counter + 1};
})

this.setState((prevState, props) => {
  return {counter: prevState.counter + props.step};
})
```

- **setState is asynchronous!!** The second parameter to setState() is an optional callback function that will be executed once setState is completed and the component is re-rendered. componentDidUpdate should be used instead to apply such logic in most cases.
  > src/ReviewPage.js

```
this.setState(
  { userInput: this.state.userInput.trim() },
  this.displayResult
)
```

