<script>
  import { Router, Route, Link } from 'svelte-routing';

  import Users from '../users/Users.svelte';
  import UsersRegister from '../users/Register.svelte';

  export let url = '';
</script>

<Router {url}>
  <nav class="navbar-fixed teal lighten-1">
    <div class="nav-wrapper">
      <ul class="right">
        <li>
          <Link to="/users">Users</Link>
        </li>
        <li>
          <Link to="/users/add">Add User</Link>
        </li>
      </ul>
    </div>
  </nav>
  <main class="container">
    <Route path="users" component={Users} />
    <Route path="users/add" component={UsersRegister} />
  </main>
</Router>
