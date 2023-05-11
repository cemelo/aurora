<script lang='ts'>
  import { Map } from '@beyonk/svelte-mapbox';

  import { getContext, onMount } from 'svelte';
  import { contextKey } from '@beyonk/svelte-mapbox';
  import MapboxTraffic from '@mapbox/mapbox-gl-traffic';

  const { getMap } = getContext(contextKey);
  const map: Map = getMap();
  //const mapbox = getMapbox()

  export let position = 'top-right';

  export let options: { showTraffic: boolean, showTrafficButton: boolean } = {
    showTraffic: true,
    showTrafficButton: false
  };

  const traffic = new MapboxTraffic(options);

  onMount(() => {
    map.addControl(traffic, position);

    // We need to toggle traffic twice to make it being displayed if showTraffic is true
    traffic.toggleTraffic();
    traffic.toggleTraffic();
  });
</script>