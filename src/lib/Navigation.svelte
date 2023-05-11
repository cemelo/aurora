<div class={`${clazz || ''}`}>
  <Map
    accessToken='pk.eyJ1IjoiY2VtZWxvIiwiYSI6ImNsaGZkZHNmaTE1dG4zZGxrNDF4c240aXUifQ.Vn0jihRLYx2dBwrb8DcilQ'
    bind:this={mapComponent}
    on:recentre={(e) => console.log(e.detail.center.lat, e.detail.center.lng)}
    options={{ scrollZoom: true, style: 'mapbox://styles/cemelo/clhfdim7g02dn01p8cenz57an' }}
  >
    <GeolocateControl options={{ some: 'control-option' }} on:eventname={eventHandler} />
    <Directions />

  </Map>
</div>

<script lang="ts">
  import { Map, Geocoder, Marker, controls } from '@beyonk/svelte-mapbox';
  import { onMount } from 'svelte';
  import Traffic from '$lib/map/Traffic.svelte';
  import Directions from '$lib/map/Directions.svelte';

  const { GeolocateControl, NavigationControl, ScaleControl } = controls;

  let clazz;
  export { clazz as class };

  let mapComponent: Map;
  let someLat = '-15.756377';
  let someLng = '-47.887187';

  onMount(async () => {
    mapComponent.setCenter([someLng, someLat]);
  });

  // Usage of methods like setCenter and flyto
  //mapComponent.setCenter([someLng, someLat]); // zoom is optional
  //mapComponent.flyTo({ center: [someLng, someLat] }); // documentation (https://docs.mapbox.com/mapbox-gl-js/example/flyto)

  // Define this to handle `eventname` events - see [GeoLocate Events](https://docs.mapbox.com/mapbox-gl-js/api/markers/#geolocatecontrol-events)
  function eventHandler(e) {
    const data = e.detail;
    // do something with `data`, it's the result returned from the mapbox event
  }
</script>

<style lang='postcss'>
  :global(.mapboxgl-ctrl-logo), :global(.mapboxgl-ctrl-attrib) {
      display: none !important;
  }
</style>