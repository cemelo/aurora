<main class="text-slate-50">
  <slot />
</main>

<script>
  import '../app.css';
</script>

<style lang="postcss">
  @import url('https://fonts.cdnfonts.com/css/satoshi');

  main {
    font-family: 'Satoshi', sans-serif;
    font-size: 0.7em;

    overflow: hidden;
    height: 100vh;
    width: 100vw;
  }
</style>
