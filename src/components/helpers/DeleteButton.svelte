<script>
  import { createEventDispatcher } from "svelte";
  let fire = createEventDispatcher();
  let confirm = false;

  const confirmDelete = () => (confirm = true);

  const cancelConfirm = () => (confirm = false);

  const confirmed = (event) => {
    confirm = false;
    fire("delete", event);
  };
</script>

{#if confirm}
  <button
    type="button"
    on:click={(event) => cancelConfirm()}
    class="btn btn-success">Cancel</button
  >
  <button type="button" on:click={(event) => confirmed()} class="btn btn-danger"
    >Sure?</button
  >
{:else}
  <button
    type="button"
    on:click={(event) => confirmDelete(event)}
    class="btn btn-danger btn-sm"
  >
    <b>X</b>
  </button>
{/if}
