<div class="content grid grid-cols-12 grid-rows-6 gap-4">
  <Greetings class="col-start-1 col-end-8 row-start-1 row-end-3" />

  <!-- Rooms -->
  <div class="card-container grid gap-4 grid-cols-3 col-start-1 col-end-8 row-start-3 row-end-7">
    <div class="card">Card 01</div>

    <div class="card">Card 02</div>

    <div class="card">Card 03</div>

    <div class="card">Card 03</div>

    <div class="card">Card 03</div>

    <div class="card">Card 03</div>

    <div class="card">Card 03</div>
  </div>

  <Navigation class="col-start-8 col-end-13 row-start-1 row-end-4"/>

  <div class="col-start-8 col-end-13 row-start-4 row-end-7">Hi Fulano, Have a great day!</div>
</div>

<script>
  import Greetings from '$lib/Greetings.svelte';
  import Navigation from '$lib/Navigation.svelte';
</script>

<style lang="postcss">
  .content {
    height: 100%;
  }

  .card-container {
    overflow-y: scroll;
  }

  .card {
    height: 120px;
  }
</style>
