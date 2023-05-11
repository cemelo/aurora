<Card class='standard-light'>
  <div slot='controls'>Controls</div>
  <div slot='info' class='info grid grid-cols-3 grid-rows-2 p-2'>
    <h3 class='col-start-1 col-end-3 font-medium'>Standard Light</h3>
    <div class='col-start-1 col-span-2'>4 devices</div>

    <div class='flex items-center justify-end col-start-3 col-end-4 row-start-1 row-end-3'>
      <button on:click={togglePower}
              class:poweredOn={deviceStatus === LightStatus.ON}
              class='power-button flex items-center justify-center rounded-md w-4/5 h-full'>
        <PoweroffOutlined />
      </button>
    </div>
  </div>
</Card>

<script lang='ts'>
  import Card from '$lib/cards/Card.svelte';
  import { PoweroffOutlined } from 'svelte-ant-design-icons';
  import { LightStatus } from '$lib/devices/lights/LightStatus.js';

  let deviceStatus: LightStatus = LightStatus.OFF;

  function togglePower() {
    switch (deviceStatus) {
      case LightStatus.ON:
        deviceStatus = LightStatus.OFF;
        break;
      case LightStatus.OFF:
        deviceStatus = LightStatus.ON;
        break;
      default:
    }
  }
</script>

<style lang='postcss'>
    h3 {
        white-space: nowrap;
        text-overflow: ellipsis;
    }

    .info button.poweredOn {
        background: rgba(200, 255, 200, 0.2);
    }

    .info button:active {
        background: rgba(255, 255, 255, 0.5);
    }
</style>
