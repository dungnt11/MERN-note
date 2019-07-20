# Redirect trong component

Để chuyển hướng trong component ta sẽ dùng ```withRouter```  kết hợp tạo hàm chuyển hướng rồi truyền cho thằng con thông qua props

```component cha```  

```javascript import { Route, Redirect, Switch, withRouter } from "react-router-dom";
import { Route, Redirect, Switch, withRouter } from "react-router-dom";
...
handleClick = url => {
    this.props.history.push(url);
  };
...
<Switch>
	<Route
          path="/ask"
          render={() =>
            isLogin ? (
              <Ask handleClick={this.handleClick} />
            ) : (
              <Redirect to="/" />
            )
          }
        />
</Switch>
...
export default connect(
  mapStateToProps,
  null
)(withRouter(Routers));
```

```component con``` sẽ dùng thằng props kia để redirect