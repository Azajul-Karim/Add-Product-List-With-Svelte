<script>
  export let text = "ADD";
  export let saved_text = "ADDED";

  export let tracker = {
    saving: false,
    saved: false,
  };

  $: if (tracker.saved) {
    setTimeout(() => {
      tracker = {
        saving: false,
        saved: false,
      };
    }, 1000);
  }
</script>

<button
  type="submit"
  class="btn btn-dark btn-block"
  disabled={tracker.saving || tracker.saved}
>
  {#if tracker.saving}
    <span class="spinner-border spinner-border-sm" role="status" />
  {:else}
    {tracker.saved ? saved_text : text}
  {/if}
</button>
