<div class={`rooms flex flex-col gap-4 ${clazz || ''}`}>
  <div class="room-selector text-lg font-medium">
    <ul class="flex flex-row justify-items-center items-center gap-3 h-full">
      {#each rooms as room}
        <li class:selected={room.selected}><button>{room.name}</button></li>
      {/each}
    </ul>
  </div>

  <div class="card-container grow grid gap-4 grid-cols-3 gradient-scroll-v">
    <StandardLightCard />
    <DimmableLightCard />
    <StandardLightCard />
    <StandardLightCard />
    <StandardLightCard />
    <StandardLightCard />
    <StandardLightCard />
  </div>
</div>

<script lang="ts">
  import StandardLightCard from '$lib/devices/lights/StandardLightCard.svelte';
  import DimmableLightCard from '$lib/devices/lights/DimmableLightCard.svelte';

  let clazz;
  export { clazz as class };

  let rooms = [
    { name: 'Living Room', selected: true },
    { name: 'Master Suite', selected: false },
    { name: 'Bedroom 1', selected: false },
    { name: 'Bedroom 2', selected: false },
    { name: 'Office', selected: false },
    { name: 'Studio', selected: false },
  ];
</script>

<style lang="postcss">
  .card-container {
    overflow-y: scroll;
  }

  .card-container :global(.card) {
    height: 120px;
  }

  .room-selector {
    overflow-x: scroll;
    height: 3em;
  }

  .room-selector li.selected {
    border-bottom: 2px solid #fff;
  }

  .room-selector li button {
    white-space: nowrap;
  }
</style>
