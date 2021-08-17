<script>
  export let disabled = false;
</script>

<button on:click {disabled}><slot /></button>

<style>
  button {
    background-color: #ffffff;
    color: rgb(10, 10, 10);
    padding: 0.5rem;
  }

  button:disabled {
    background-color: rgb(197, 194, 194);
  }
</style>
