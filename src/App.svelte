<script>
  import Header from './Header.svelte';
  import Footer from './Footer.svelte';
  import Button from './Button.svelte';
  import Kuva from './Kuva.svelte';
  import Haku from './Haku.svelte';
  import Hakuhistoria from './Hakuhistoria.svelte';
  import Hakuvinkit from './Hakuvinkit.svelte';
  export let name;

  let promise;
  let naytaHistoria = false;
  let naytaVinkit = false;

  function searchResult(event) {
    promise = event.detail;
  }
</script>

<Header {name} />
<main>
  <Kuva {promise} />
  <Haku on:searchResult={searchResult} />
  <Button on:click={() => (naytaHistoria = !naytaHistoria)}>
    Hakuhistoria
  </Button>
  <Button on:click={() => (naytaVinkit = !naytaVinkit)}>Hakuvinkit</Button>
  {#if naytaHistoria}
    <Hakuhistoria />
  {/if}
  {#if naytaVinkit}
    <Hakuvinkit />
  {/if}
</main>
<Footer />

<style>
  main {
    text-align: center;
    padding: 1rem;
    margin: 0 auto;
  }
</style>
