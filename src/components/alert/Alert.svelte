<script>
  export let message;
</script>

<style>
  .message {
    padding: 20px 0;
  }
</style>

{#if message}
  <div class="red lighten-1" role="alert">
    <p class="message white-text center-align">{message}</p>
  </div>
{/if}
