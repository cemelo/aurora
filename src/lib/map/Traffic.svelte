<script lang="ts">
  import { Map } from '@beyonk/svelte-mapbox';

  import { getContext, onDestroy, onMount } from 'svelte';
  import { contextKey } from '@beyonk/svelte-mapbox';
  import MapboxTraffic from '@mapbox/mapbox-gl-traffic/mapbox-gl-traffic';

  const { getMap } = getContext(contextKey);
  const map: Map = getMap();
  //const mapbox = getMapbox()

  export let position = 'top-right';

  export let options: { showTraffic: boolean; showTrafficButton: boolean } = {
    showTraffic: true,
    showTrafficButton: false,
  };

  const traffic = new MapboxTraffic(options);

  onMount(() => {
    map.addControl(traffic, position);
    traffic.render();
  });

  onDestroy(() => {
    map.removeControl(traffic);
  });
</script>
