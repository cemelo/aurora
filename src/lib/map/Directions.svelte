<script lang='ts'>
  import { Map } from '@beyonk/svelte-mapbox';
  import MapboxDirections from '@mapbox/mapbox-gl-directions/dist/mapbox-gl-directions';
  import '@mapbox/mapbox-gl-directions/dist/mapbox-gl-directions.css';

  import { getContext, onMount } from 'svelte';
  import { contextKey } from '@beyonk/svelte-mapbox';

  const { getMap, getMapbox } = getContext(contextKey);
  const map: Map = getMap();
  const mapbox = getMapbox();

  export let position = 'top-right';

  export let options = {
    accessToken: 'pk.eyJ1IjoiY2VtZWxvIiwiYSI6ImNsaGZkZHNmaTE1dG4zZGxrNDF4c240aXUifQ.Vn0jihRLYx2dBwrb8DcilQ',
    unit: 'metric',
    profile: 'mapbox/driving-traffic',
    congestion: true,
    interactive: false,
    controls: {
      inputs: false,
      instructions: false,
      profileSwitcher: false
    },
    flyTo: true
  };

  const directions = new MapboxDirections(options);

  map.addControl(directions, position);

  onMount(async () => {
    setTimeout(async () => {
      directions.setOrigin('SQN 110 Bloco M, Brasília - DF, Brasil');
      directions.setDestination('Complexo da Polícia Civil do Distrito Federal, Brasília - DF, Brasil');

      setTimeout(() => {
        directions.reverse();

        setTimeout(() => {
          directions.reverse();
        });
      });
    }, 1000);
  });
</script>