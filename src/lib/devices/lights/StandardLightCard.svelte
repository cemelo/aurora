<Card
  on:click={togglePower}
  class="standard-light grid grid-cols-3 grid-rows-3 p-2"
  style="--light-status-color: {lightStatusColor}"
>
  <div class="status col-start-4 row-start-1">&nbsp;</div>

  <div class="flex justify-center items-center col-span-4 col-start-1 row-start-1 row-span-2">
    {#if deviceStatus === LightStatus.OFF}
      <LightbulbOffFill height={28} width={28} />
    {:else if deviceStatus === LightStatus.ON}
      <LightbulbFill height={28} width={28} />
    {/if}
  </div>

  <div class="col-start-1 col-span-4 row-start-3 justify-center items-center">
    <h3 class="text-center font-bold">Standard Light</h3>
    <div class="text-center">4 devices</div>
  </div>
</Card>

<script lang="ts">
  import Card from '$lib/Card.svelte';
  import { LightbulbFill, LightbulbOffFill } from 'svelte-bootstrap-icons';
  import { LightStatus } from '$lib/devices/lights/LightStatus.js';

  let deviceStatus: LightStatus = LightStatus.OFF;
  let lightStatusColor = '#ff7272';

  function togglePower() {
    switch (deviceStatus) {
      case LightStatus.ON:
        deviceStatus = LightStatus.OFF;
        lightStatusColor = '#ff7272';
        break;
      case LightStatus.OFF:
        deviceStatus = LightStatus.ON;
        lightStatusColor = '#42ffc6';
        break;
      default:
    }
  }
</script>

<style lang="postcss">
  .standard-light {
    color: black !important;
  }

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

  .status {
    background-color: var(--light-status-color, #42ffc6);
    transition: background-color 0.25s ease;

    border-radius: 5px;
    width: 10px;
    height: 10px;
  }
</style>
