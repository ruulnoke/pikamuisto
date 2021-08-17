<script>
  import { fade, fly } from 'svelte/transition';
  import hakusanat from './store';
</script>

<div in:fly={{ y: 100, duration: 2000 }} out:fade>
  {#if $hakusanat.length < 1}
    <p>Ei hakuja</p>
  {:else}
    {#each $hakusanat as hakusana}
      <p>{hakusana}</p>
    {/each}
  {/if}
</div>
