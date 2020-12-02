<script>
  import { onMount } from 'svelte';
  import { navigate } from 'svelte-routing';

  import API_ROUTES from '../../utils/apiRoutes';
  import * as routes from '../router/routes';

  export let users = null;

  // TODO:add loading indicator
  // TODO: add error message

  function getUsers() {
    fetch(`${process.env.API_BASE}${API_ROUTES.user}`)
      .then((response) => response.json())
      .then((data) => {
        users = data;
      })
      .catch(() => {
        users = null;
      });
  }

  onMount(() => {
    getUsers();
  });

  function onUpdateClickFactory(user) {
    return function handleOnUpdateClick() {
      navigate(`${routes.EDIT_USER}/${user.id}`, { state: { user } });
    };
  }

  function onDeleteClickFactory(user) {
    return function handleOnDeleteClick() {
      fetch(`${process.env.API_BASE}${API_ROUTES.user}`, {
        method: 'DELETE',
        body: new URLSearchParams({
          id: user.id,
        }),
      })
        .then(getUsers)
        .catch(console.error);
    };
  }
</script>

{#if users}
  <table>
    <thead>
      <tr>
        <th>First name</th>
        <th>Last name</th>
        <th>Email</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      {#each users as user}
        <tr>
          <td>{user.firstName}</td>
          <td>{user.lastName || '-'}</td>
          <td>{user.email}</td>
          <td>
            <button
              class="btn waves-effect waves-light"
              type="button"
              on:click={onUpdateClickFactory(user)}>Update
            </button>
            <button
              class="btn waves-effect waves-light red lighten-1"
              type="button"
              on:click={onDeleteClickFactory(user)}>Remove
            </button>
          </td>
        </tr>
      {/each}
    </tbody>
  </table>
{/if}
