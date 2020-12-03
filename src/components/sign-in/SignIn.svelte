<script>
  import { navigate } from 'svelte-routing';

  import API_ROUTES from '../../utils/apiRoutes';
  import * as routes from '../router/routes';

  let email;
  let password;

  function handleOnSubmit(event) {
    event.preventDefault();

    if (!email || !password) {
      return;
    }

    fetch(`${process.env.API_BASE}${API_ROUTES.signIn}`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
      },
      body: new URLSearchParams({
        email,
        password,
      }),
    })
      .then((response) => {
        if (response.status === 200) {
          navigate(routes.USERS);
        } else {
          console.error('Unautorizhed...');
        }
      })
      .catch(console.error);
  }
</script>

<style>
  .hiddenLabel {
    position: absolute;
    width: 1px;
    height: 1px;
    overflow: hidden;
    clip: rect(1px, 1px, 1px, 1px);
    clip-path: inset(50%);
  }
</style>

<div class="row">
  <form on:submit={handleOnSubmit} class="col s6 push-s3">
    <div class="row">
      <div class="input-field col s12">
        <input placeholder="Email" id="email" type="email" bind:value={email} />
        <label for="email" class="hiddenLabel">Email</label>
      </div>
    </div>
    <div class="row">
      <div class="input-field col s12">
        <input
          placeholder="Password"
          id="password"
          type="password"
          bind:value={password} />
        <label for="password" class="hiddenLabel">Password</label>
      </div>
    </div>
    <button class="btn waves-effect waves-light" type="submit">Sign in</button>
  </form>
</div>
