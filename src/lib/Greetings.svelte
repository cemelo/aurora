<div class={`greetings ${clazz || ''}`}>
  <div class="weather flex gap-4">
    <div class="flex justify-items-center items-center">
      <img alt="Humidity" class="humidity-icon filter-light-blue" src={humidity} />
      <div class="indicator-text">55%</div>
    </div>

    <div class="flex justify-items-center items-center">
      <img alt="Temperature" class="temperature-icon" src={thermometer} />
      <div class="indicator-text">19&deg;</div>
    </div>

    <div class="flex justify-items-center items-center">
      <img alt="Temperature" class="temperature-icon" src={cloudy} />
      <div class="indicator-text">Cloudy</div>
    </div>
  </div>
  <h1>
    Hi {name},<br />
    Have a great day!
  </h1>
</div>

<script>
  import humidity from '$lib/assets/weather/humidity.svg';
  import thermometer from '$lib/assets/weather/thermometer.svg';
  import cloudy from '$lib/assets/weather/cloudy.svg';

  let clazz;
  let name = 'Rosana';

  export { clazz as class };
</script>

<style>
  .greetings h1 {
    font-size: 1.8em;
  }

  .weather {
    margin-bottom: 15px;
  }

  .weather img {
    height: 24px;
    width: auto;
  }

  .weather .indicator-text {
    font-weight: 400;
  }

  .filter-light-blue {
    filter: brightness(0) saturate(100%) invert(81%) sepia(74%) saturate(3187%) hue-rotate(176deg)
      brightness(102%) contrast(102%);
  }
</style>
