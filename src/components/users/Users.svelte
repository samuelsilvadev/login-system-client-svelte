<script>
  import { onMount } from 'svelte';

  import API_ROUTES from '../../utils/apiRoutes';

  export let users = null;

  // TODO:add loading indicator
  // TODO: add error message

  onMount(() => {
    fetch(`${process.env.API_BASE}${API_ROUTES.user}`)
      .then((response) => response.json())
      .then((data) => {
        users = data;
      })
      .catch(() => {
        users = null;
      });
  });
</script>

{#if users}
  <table>
    <thead>
      <tr>
        <th>First name</th>
        <th>Last name</th>
        <th>Email</th>
      </tr>
    </thead>
    <tbody>
      {#each users as user}
        <tr>
          <td>{user.firstName}</td>
          <td>{user.lastName || '-'}</td>
          <td>{user.email}</td>
        </tr>
      {/each}
    </tbody>
  </table>
{/if}
