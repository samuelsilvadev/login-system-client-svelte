<script>
  import { navigate } from 'svelte-routing';

  import Alert from '../alert/Alert.svelte';

  import API_ROUTES from '../../utils/apiRoutes';
  import * as routes from '../router/routes';

  let email;
  let password;
  let errorMessage;

  function handleOnSubmit(event) {
    event.preventDefault();

    errorMessage = undefined;

    if (!email || !password) {
      errorMessage = 'You need to fill email and password';
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
          errorMessage = 'Email or password are incorrects';
        }
      })
      .catch(() => {
        errorMessage = 'Something went wrong';
      });
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
  <Alert message={errorMessage} />
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
