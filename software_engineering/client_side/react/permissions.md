# Client-side Permission patterns in React

1. JavaScript lazy permission checking
Scenario: Not all permissions available at render() time. Want to check permissions before attempting action.

```javascript
function userAttemptedToRunCommandWithoutClusterErrorHandler(user) {
  withPermissions([Cluster], (clusterPermissions) => {
    const userOptions = [];
    if (clusterPermissions.canAttach())
      userOptions.push(Cluster.forUser(user));
    if (clusterPermissions.canCreate())
      userOptions.push(Cluster.createDialog(user));
      
    renderTheUsersOptions(userOptions);
  }
}
```

1. React render time wrapper
```javascript
class UserAttemptedToRunCommandWithoutClusterErrorHandler {
  render() {
    return (
      <div>
        <Permissions class={Cluster} permissions={['attach']}>
          <AttachToClusterList />
        </Permissions>
        <Permissions class={Cluster} permissions={['create']}>
          <CreateClusterList />
        </Permissions>
      </div>
    );
  }
}
```

1. React prop
```javascript
class UserAttemptedToRunCommandWithoutClusterErrorHandler {
  render() {
    const clusterPermissions = this.props.clusterPermissions;
    return (
      <div>
        { clusterPermissions.canAttach() ? <AttachToClusterList /> : null }
        { clusterPermissions.canCreate() ? <CreateClusterList /> : null }
      </div>
    );
  }
}
```
