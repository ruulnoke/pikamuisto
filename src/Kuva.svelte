<script>
  import { Circle } from 'svelte-loading-spinners';
  export let promise;
</script>

<main>
  {#if promise}
    {#await promise}
      <div class="spinner">
        <Circle size="60" color="#FF3E00" unit="px" duration="1s" />
      </div>
    {:then image}
      <img src={'https://www.finna.fi' + image.images[0]} alt="päivän kuva" />
      <p class="sourceInfo">
        {#if image.nonPresenterAuthors[0]}
          {image.title}.
          <span class="capitalize">{image.nonPresenterAuthors[0].role}</span>
          {image.nonPresenterAuthors[0].name}.
        {:else}
          {image.title}. Ei tekijätietoja.
        {/if}
        {#if image.buildings[1]}
          {image.buildings[1].translated}, {image.buildings[0].translated}.
        {:else}
          {image.buildings[0].translated}.
        {/if}
      </p>
    {:catch error}
      <p style="color: red">{error.message}</p>
    {/await}
  {/if}
</main>

<style>
  img {
    max-width: 100%;
  }

  .spinner {
    margin: auto;
    width: 60px;
  }

  .sourceInfo {
    font-style: italic;
    margin-bottom: 4rem;
  }

  .sourceInfo::first-letter {
    text-transform: capitalize;
  }

  .capitalize {
    text-transform: capitalize;
  }
</style>
