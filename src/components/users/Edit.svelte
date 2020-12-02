<script>
  import { onMount } from 'svelte';
  import { navigate } from 'svelte-routing';

  import API_ROUTES from '../../utils/apiRoutes';
  import * as routes from '../router/routes';

  export let id = null;
  let firstName = '';
  let lastName = '';
  let email = '';
  let password = '';

  onMount(() => {
    if (typeof window !== 'undefined') {
      const { user } = window.history.state || {};

      firstName = user.firstName;
      lastName = user.lastName;
      email = user.email;
    }
  });

  function handleSubmit(event) {
    event.preventDefault();

    // TODO:add loading indicator
    // TODO: add error message

    fetch(`${process.env.API_BASE}${API_ROUTES.user}`, {
      method: 'PUT',
      body: new URLSearchParams({
        id,
        firstName,
        lastName,
        email,
        password,
      }),
    })
      .then(() => {
        navigate(routes.USERS);
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
  <form on:submit={handleSubmit} class="col s12">
    <div class="row">
      <div class="input-field col s12">
        <input
          placeholder="First Name"
          id="first-name"
          type="text"
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
          bind:value={lastName} />
        <label for="last-name" class="hiddenLabel">Last Name</label>
      </div>
    </div>
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
          bind:value={password}
          autocomplete="current-password" />
        <label for="password" class="hiddenLabel">Password</label>
      </div>
    </div>
    <button class="btn waves-effect waves-light" type="submit">Submit </button>
  </form>
</div>
