<div class={`${clazz || ''}`}>
  <Map
    accessToken="pk.eyJ1IjoiY2VtZWxvIiwiYSI6ImNsaGZkZHNmaTE1dG4zZGxrNDF4c240aXUifQ.Vn0jihRLYx2dBwrb8DcilQ"
    bind:this={mapComponent}
    options={{ scrollZoom: true, style: 'mapbox://styles/cemelo/clhfdim7g02dn01p8cenz57an' }}
  >
    <Directions />
    <Traffic />
  </Map>
</div>

<script lang="ts">
  import { onMount } from 'svelte';
  import { Map } from '@beyonk/svelte-mapbox';

  import Traffic from '$lib/map/Traffic.svelte';
  import Directions from '$lib/map/Directions.svelte';

  let clazz;
  export { clazz as class };

  let mapComponent: Map;
  let someLat = '-15.756377';
  let someLng = '-47.887187';

  onMount(async () => {
    mapComponent.setCenter([someLng, someLat]);
  });
</script>

<style lang="postcss">
  :global(.mapboxgl-ctrl-logo),
  :global(.mapboxgl-ctrl-attrib) {
    display: none !important;
  }
</style>
