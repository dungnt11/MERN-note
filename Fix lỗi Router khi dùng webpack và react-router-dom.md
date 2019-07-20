# Fix lỗi Router khi dùng webpack và react-router-dom

Chuyển sang dùng HashRouter

```js
import React, { Component } from "react";
import { HashRouter, Route, Link } from "react-router-dom";

export default class App extends Component {
  render() {
    return (
      <HashRouter>
        <Link to="/">Home</Link>
        <Route path="/" exact component={() => <h1>Hello</h1>} />
      </HashRouter>
    );
  }
}
```

