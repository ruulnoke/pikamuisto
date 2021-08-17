<script>
  import { fade, fly } from 'svelte/transition';
</script>

<main in:fly={{ y: 100, duration: 2000 }} out:fade>
  <p>
    Hae yhdellä tai useammalla sanalla. Kokeile myös numeroita. Kirjoita
    esimerkiksi "jyväskylä koira" tai "22b". Tulokset saattavat yllättää.
  </p>
  <p>
    Jokainen haku tuo vastaukseksi ensimmäisen sopivan kuvan, jolla on lisenssi
    CC BY 4.0. Tismalleen samalla haulla voi saada erilaisen tuloksen vain
    Finnan tietokannan päivittyessä.
  </p>
</main>

<style>
  p {
    text-align: left;
  }
</style>
