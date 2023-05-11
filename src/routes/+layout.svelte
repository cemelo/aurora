<main class="p-4">
  <slot />
</main>

<script>
  import '../app.css';
</script>

<style lang="postcss">
  @import url('https://fonts.cdnfonts.com/css/satoshi');

  main {
    background: linear-gradient(178.1deg, rgb(60, 55, 106) 8.5%, rgb(23, 20, 69) 82.4%);
    color: #f0f0f0;
    font-family: 'Satoshi', sans-serif;
    font-size: 0.7em;

    overflow: hidden;
    height: 100vh;
    width: 100vw;
  }
</style>
