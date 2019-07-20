# Private Component

```PrivateComponent.js```	

```javascript
import React from 'react';
import { Route, Redirect } from 'react-router-dom';
import { connect } from 'react-redux';
import PropTypes from 'prop-types';

const PrivateRoute = ({ component: Component, auth, ...rest }) => (
  <Route
    {...rest}
    render={props =>
      auth.isAuthenticated === true ? (
        <Component {...props} />
      ) : (
        <Redirect to="/login" />
      )
    }
  />
);

PrivateRoute.propTypes = {
  auth: PropTypes.object.isRequired
};

const mapStateToProps = state => ({
  auth: state.auth
});

export default connect(mapStateToProps)(PrivateRoute);

```

Example component use this

```javascript
<Switch>
    <PrivateRoute
    exact
    path="/create-profile"
    component={CreateProfile}
    />
</Switch>
```

Bọc trong ```<Switch>``` để đảm bảo chỉ có 1 component được render