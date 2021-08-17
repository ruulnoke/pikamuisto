<script>
  import { createEventDispatcher } from 'svelte';
  import hakusanat from './store.js';
  import Button from './Button.svelte';

  const dispatch = createEventDispatcher();

  let keyword = '';
  $: valid = keyword.trim().length > 0;

  async function search() {
    const response = await fetch(
      `https://api.finna.fi/api/v1/search?lookfor=${keyword}&type=AllFields&filter%5B%5D=format%3A1%2FImage%2FImage%2F&sort=relevance%2Cid%20asc&page=1&limit=100&prettyPrint=false&lng=fi`
    );
    const images = await response.json();
    if (response.ok) {
      if (typeof images.records === 'undefined') {
        throw new Error('Kuvaa ei löydy. Kokeile toista hakusanaa.');
      }
      let chosenImage = images.records.find(
        (element) =>
          'imageRights' in element &&
          element.imageRights.copyright == 'CC BY 4.0'
      );
      if (typeof chosenImage === 'undefined') {
        throw new Error('Kuvaa ei löydy. Kokeile toista hakusanaa.');
      }
      return chosenImage;
    } else {
      throw new Error('Virhe haettaessa tietoja');
    }
  }

  function startSearch() {
    let promise = search();
    dispatch('searchResult', promise);
    hakusanat.update((hakusanat) => [...hakusanat, keyword]);
    console.log(hakusanat);
  }
</script>

<main>
  <p>Hae yhdellä tai useammalla hakusanalla.</p>
  <input type="text" id="keyword" name="keyword" bind:value={keyword} />
  <Button on:click={startSearch} disabled={!valid}>Haku</Button>
</main>
