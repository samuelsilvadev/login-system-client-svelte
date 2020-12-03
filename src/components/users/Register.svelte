<script>
  import { navigate } from 'svelte-routing';

  import Alert from '../alert/Alert.svelte';

  import API_ROUTES from '../../utils/apiRoutes';

  let firstName = '';
  let lastName = '';
  let email = '';
  let password = '';
  let errorMessage;

  function handleSubmit(event) {
    event.preventDefault();

    errorMessage = undefined;

    // TODO:add loading indicator

    fetch(`${process.env.API_BASE}${API_ROUTES.user}`, {
      method: 'POST',
      headers: {
        'Content-Type': 'application/x-www-form-urlencoded',
      },
      body: new URLSearchParams({
        firstName,
        lastName,
        email,
        password,
      }),
    })
      .then(() => {
        navigate(routes.USERS);
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
  <form on:submit={handleSubmit} class="col s12">
    <div class="row">
      <div class="input-field col s12">
        <input
          placeholder="First Name"
          id="first-name"
          type="text"
          required
          bind:value={firstName} />
        <label for="first-name" class="hiddenLabel">First Name</label>
      </div>
    </div>
    <div class="row">
      <div class="input-field col s12">
        <input
          placeholder="Last Name"
          id="last-name"
          type="text"
          required
          bind:value={lastName} />
        <label for="last-name" class="hiddenLabel">Last Name</label>
      </div>
    </div>
    <div class="row">
      <div class="input-field col s12">
        <input
          placeholder="Email"
          id="email"
          type="email"
          required
          bind:value={email} />
        <label for="email" class="hiddenLabel">Email</label>
      </div>
    </div>
    <div class="row">
      <div class="input-field col s12">
        <input
          placeholder="Password"
          id="password"
          type="password"
          required
          bind:value={password}
          autocomplete="current-password" />
        <label for="password" class="hiddenLabel">Password</label>
      </div>
    </div>
    <button class="btn waves-effect waves-light" type="submit">Submit</button>
  </form>
</div>
