<script>
  import API_ROUTES from '../../utils/apiRoutes';

  let firstName = '';
  let lastName = '';
  let email = '';
  let password = '';

  function handleSubmit(event) {
    event.preventDefault();

    // TODO:add loading indicator
    // TODO: add error message

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
      .then(console.log)
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
          bind:value={password} />
        <label for="password" class="hiddenLabel">Password</label>
      </div>
    </div>
    <button
      class="btn waves-effect waves-light"
      type="submit"
      name="action">Submit
    </button>
  </form>
</div>
