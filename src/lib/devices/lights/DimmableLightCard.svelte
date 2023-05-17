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
    <h3 class="text-center font-bold">Dimmable Light</h3>
    <div class="text-center">4 devices</div>
  </div>
</Card>

<svelte:window on:click|stopPropagation|preventDefault={closeDialog} />

<dialog bind:this={settingsDialog} class="light-settings-dialog w-3/4 h-4/5 text-slate-50">
  <div class="flex flex-col justify-center items-center w-full h-full">
    <div>
      <h3 class="text-base font-extrabold">Living Room - Dimmable Light</h3>
    </div>
    <div class="brightness-slider flex flex-col justify-center items-center grow p-5 gap-4">
      <BrightnessHigh height={28} width={28} />
      <VerticalSlider />
      <BrightnessLow height={28} width={28} />
    </div>
    <div>
      <button>
        <Power height={28} width={28} />
      </button>
    </div>
  </div>
</dialog>

<script lang="ts">
  import Card from '$lib/Card.svelte';
  import { LightbulbFill, LightbulbOffFill, Power, BrightnessLow, BrightnessHigh } from 'svelte-bootstrap-icons';
  import { LightStatus } from '$lib/devices/lights/LightStatus.js';
  import { onMount } from 'svelte';
  import VerticalSlider from '$lib/components/VerticalSlider.svelte';

  let settingsDialog: HTMLDialogElement;

  let deviceStatus: LightStatus = LightStatus.OFF;
  let lightStatusColor = '#ff7272';

  function togglePower() {
    settingsDialog.showModal();
  }

  function closeDialog(e: Event) {
    if (!settingsDialog.open) {
      console.log('dialog not open');
      return;
    } else {
      console.log('dialog open');
    }

    if (e.target !== settingsDialog && settingsDialog.contains(e.target as Node)) {
      return;
    }

    settingsDialog.close();
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

  .light-settings-dialog {
    background-color: rgba(0, 0, 0, 0.6);
    backdrop-filter: blur(20px);
  }

  .light-settings-dialog[open] {
    animation-name: opacity-animation;
    animation-duration: 300ms;
    animation-timing-function: ease;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  .light-settings-dialog[open]::backdrop {
    animation-name: backdrop-filter-animation;
    animation-duration: 300ms;
    animation-timing-function: ease;
    animation-iteration-count: 1;
    animation-fill-mode: forwards;
  }

  @keyframes opacity-animation {
    from {
      opacity: 0;
    }

    to {
      opacity: 1;
    }
  }

  @keyframes backdrop-filter-animation {
    from {
      backdrop-filter: blur(0px);
    }

    to {
      backdrop-filter: blur(5px);
    }
  }
</style>
