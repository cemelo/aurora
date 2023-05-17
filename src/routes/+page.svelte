<div class="content grid grid-cols-12 grid-rows-6 gap-4 w-full h-full p-4">
  <Greetings class="col-start-1 col-end-8 row-start-1 row-end-3" />

  <!-- Rooms -->
  <Rooms class="col-start-1 col-end-8 row-start-3 row-end-7" />

  <Navigation class="col-start-8 col-end-13 row-start-1 row-end-4" />

  <div class="col-start-8 col-end-13 row-start-4 row-end-7">Hi Fulano, Have a great day!</div>
</div>

<script>
  import Greetings from '$lib/Greetings.svelte';
  import Navigation from '$lib/map/Navigation.svelte';
  import Rooms from '$lib/Rooms.svelte';
</script>

<style lang="postcss">
  .content {
    background: url('$lib/assets/rooms/living-room.jpeg'), rgba(0, 0, 0, 0.5);
    background-blend-mode: multiply;
  }
</style>
