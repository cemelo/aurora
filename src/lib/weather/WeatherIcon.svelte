{#if weatherId}
  <img {width} {height} src={icon} alt={description} />
{:else}
  <div style="width: {width}; height: {height}" class="weather-icon" alt="" />
{/if}

<script lang="ts">
  import { afterUpdate, onMount } from 'svelte';

  export let weatherId: number;
  export let uvIndex: number = 0;
  export let isDay: boolean = true;
  export let description: string = '';

  export let width: string = '32px';
  export let height: string = '32px';

  let icon;

  const iconsMapping = {
    // Thunderstorms
    200: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day-rain' : 'thunderstorms-night-rain'),
    201: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day-rain' : 'thunderstorms-night-rain'),
    202: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day-rain' : 'thunderstorms-night-rain'),
    210: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day' : 'thunderstorms-night'),
    211: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day' : 'thunderstorms-night'),
    212: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day' : 'thunderstorms-night'),
    221: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day' : 'thunderstorms-night'),
    230: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day-rain' : 'thunderstorms-night-rain'),
    231: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day-rain' : 'thunderstorms-night-rain'),
    232: (_uvIndex: number, isDay: boolean) => (isDay ? 'thunderstorms-day-rain' : 'thunderstorms-night-rain'),

    // Drizzle
    300: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-drizzle' : 'partly-cloudy-night-drizzle'), // Drizzle 	light intensity drizzle 	09d
    301: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-drizzle' : 'partly-cloudy-night-drizzle'), // Drizzle 	drizzle 	09d
    302: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-drizzle' : 'partly-cloudy-night-drizzle'), // Drizzle 	heavy intensity drizzle 	09d
    310: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-drizzle' : 'partly-cloudy-night-drizzle'), // Drizzle 	light intensity drizzle rain 	09d
    311: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-hail' : 'partly-cloudy-night-hail'), // Drizzle 	drizzle rain 	09d
    312: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-hail' : 'partly-cloudy-night-hail'), // Drizzle 	heavy intensity drizzle rain 	09d
    313: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-hail' : 'partly-cloudy-night-hail'), // Drizzle 	shower rain and drizzle 	09d
    314: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-hail' : 'partly-cloudy-night-hail'), // Drizzle 	heavy shower rain and drizzle 	09d
    321: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-hail' : 'partly-cloudy-night-hail'), // Drizzle 	shower drizzle 	09d

    // Rain
    500: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-rain' : 'partly-cloudy-night-rain'), //  Rain 	light rain 	10d
    501: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day-rain' : 'partly-cloudy-night-rain'), //  Rain 	moderate rain 	10d
    502: (_uvIndex: number, isDay: boolean) => (isDay ? 'rain' : 'rain'), //  Rain 	heavy intensity rain 	10d
    503: (_uvIndex: number, isDay: boolean) => (isDay ? 'rain' : 'rain'), //  Rain 	very heavy rain 	10d
    504: (_uvIndex: number, isDay: boolean) => (isDay ? 'rain' : 'rain'), //  Rain 	extreme rain 	10d
    511: (_uvIndex: number, isDay: boolean) => (isDay ? 'sleet' : 'sleet'), //  Rain 	freezing rain 	13d
    520: (_uvIndex: number, isDay: boolean) => (isDay ? 'rain' : 'rain'), //  Rain 	light intensity shower rain 	09d
    521: (_uvIndex: number, isDay: boolean) => (isDay ? 'rain' : 'rain'), //  Rain 	shower rain 	09d
    522: (_uvIndex: number, isDay: boolean) => (isDay ? 'rain' : 'rain'), //  Rain 	heavy intensity shower rain 	09d
    531: (_uvIndex: number, isDay: boolean) => (isDay ? 'rain' : 'rain'), //  Rain 	ragged shower rain 	09d

    // Snow
    600: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	light snow 	13d
    601: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Snow 	13d
    602: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Heavy snow 	13d
    611: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Sleet 	13d
    612: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Light shower sleet 	13d
    613: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Shower sleet 	13d
    615: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Light rain and snow 	13d
    616: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Rain and snow 	13d
    620: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Light shower snow 	13d
    621: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Shower snow 	13d
    622: (_uvIndex: number, isDay: boolean) => (isDay ? 'snow' : 'snow'), // 	Snow 	Heavy shower snow 	13d

    // Atmospheric
    701: (_uvIndex: number, isDay: boolean) => (isDay ? 'mist' : 'mist'), // Mist 	mist 	50d
    711: (_uvIndex: number, isDay: boolean) => (isDay ? 'smoke' : 'smoke'), // Smoke 	Smoke 	50d
    721: (_uvIndex: number, isDay: boolean) => (isDay ? 'haze-day' : 'haze-night'), // Haze 	Haze 	50d
    731: (_uvIndex: number, isDay: boolean) => (isDay ? 'dust-day' : 'dust-night'), // Dust 	sand/ dust whirls 	50d
    741: (_uvIndex: number, isDay: boolean) => (isDay ? 'fog-day' : 'fog-night'), // Fog 	fog 	50d
    751: (_uvIndex: number, isDay: boolean) => (isDay ? 'dust-day' : 'dust-night'), // Sand 	sand 	50d
    761: (_uvIndex: number, isDay: boolean) => (isDay ? 'dust-day' : 'dust-night'), // Dust 	dust 	50d
    762: (_uvIndex: number, isDay: boolean) => (isDay ? 'mist' : 'mist'), // Ash 	volcanic ash 	50d
    771: (_uvIndex: number, isDay: boolean) => (isDay ? 'mist' : 'mist'), // Squall 	squalls 	50d
    781: (_uvIndex: number, isDay: boolean) => (isDay ? 'tornado' : 'tornado'), // Tornado 	tornado 	50d

    // Clear
    800: (uvIndex: number, isDay: boolean) => {
      if (!isDay) {
        return 'clear-night';
      } else {
        if (1 <= uvIndex && uvIndex <= 11) return `uv-index-${uvIndex}`;
        else return 'clear-day';
      }
    }, // Clear 	clear sky 	01d

    801: (_uvIndex: number, isDay: boolean) => (isDay ? 'partly-cloudy-day' : 'partly-cloudy-night'), //  Clouds 	few clouds: 11-25% 	02d
    802: (_uvIndex: number, isDay: boolean) => (isDay ? 'cloudy' : 'cloudy'), //  Clouds 	scattered clouds: 25-50% 	03d
    803: (_uvIndex: number, isDay: boolean) => (isDay ? 'overcast-day' : 'overcast-night'), //  Clouds 	broken clouds: 51-84% 	04d
    804: (_uvIndex: number, isDay: boolean) => (isDay ? 'overcast' : 'overcast'), //  Clouds 	overcast clouds: 85-100% 	04d
  };

  afterUpdate(() => {
    if (weatherId) {
      icon = `/weather/${iconsMapping[weatherId](uvIndex, isDay)}.svg`;
    }
  });
</script>
