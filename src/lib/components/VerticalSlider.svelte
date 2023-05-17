<svelte:window
  on:mousemove|stopPropagation|preventDefault={handleMouseMove}
  on:mouseup|stopPropagation|preventDefault={handleMouseUp}
  on:touchmove|stopPropagation|preventDefault={handleTouchMove}
  on:touchend|stopPropagation|preventDefault={handleTouchEnd}
/>

<div
  bind:this={container}
  on:touchstart={handleTouchStart}
  on:mousedown|stopPropagation|preventDefault={handleMouseDown}
  {...$$restProps}
  class="slider-container flex flex-row justify-center items-end ${clazz || ''}"
>
  <div class="slider-status w-full" style="--slider-percentage: {sliderPercentage}">&nbsp;</div>
</div>

<script lang="ts">
  export let start = 0;
  export let end = 100;
  export let value = 10;

  let container: HTMLDivElement;
  let touchStart = 0;
  let changing = false;

  let clazz;
  export { clazz as class };

  $: sliderPercentage = (value - start) / (end - start);

  function handleTouchStart(e: TouchEvent) {
    console.log(container.offsetHeight);
    touchStart = e.touches.item(0).clientY;
  }

  function handleTouchMove(e: TouchEvent) {
    const diff = (touchStart - e.touches.item(0).clientY) / container.offsetHeight;
    console.log(diff);
  }

  function handleTouchEnd() {
    console.log('end');
  }

  function handleMouseDown(e: MouseEvent) {
    changing = true;
    touchStart = e.clientY;
    console.log('down');
  }

  function handleMouseMove(e: MouseEvent) {
    if (changing) {
      const diff = (touchStart - e.clientY) / container.offsetHeight;
      value += diff * 100;

      value = Math.max(value, start);
      value = Math.min(value, end);

      if (value < -1 || value > 1) {
        touchStart = e.clientY;
      }
    }
  }

  function handleMouseUp() {
    changing = false;
  }
</script>

<style lang="postcss">
  .slider-container {
    background: #ffffff30;
    border-radius: 16px;
    width: 50px;
    height: 100%;
    overflow: hidden;
    user-select: none;
    cursor: default;
  }

  .slider-status {
    height: calc(var(--slider-percentage) * 100%);
    background: #ffffffaa;
  }
</style>
