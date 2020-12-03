<script>
  import { Router, Route, Link } from 'svelte-routing';

  import Users from '../users/Users.svelte';
  import UsersRegister from '../users/Register.svelte';
  import UsersEdit from '../users/Edit.svelte';
  import SignIn from '../sign-in/SignIn.svelte';

  import * as routes from './routes';

  export let url = '';
</script>

<Router {url}>
  <nav class="navbar-fixed teal lighten-1">
    <div class="nav-wrapper">
      <ul class="right">
        <li>
          <Link to={routes.USERS}>Users</Link>
        </li>
        <li>
          <Link to={routes.ADD_USER}>Add User</Link>
        </li>
        <li>
          <Link to={routes.SIGN_IN}>Sign In</Link>
        </li>
      </ul>
    </div>
  </nav>
  <main class="container">
    <Route path={routes.SIGN_IN} component={SignIn} />
    <Route path={routes.USERS} component={Users} />
    <Route path={routes.ADD_USER} component={UsersRegister} />
    <Route path={`${routes.EDIT_USER}/:id`} component={UsersEdit} />
  </main>
</Router>
