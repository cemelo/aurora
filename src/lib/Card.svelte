<div on:click {...$$restProps} class={`card flex flex-col ${clazz || ''}`}>
  <slot />
</div>

<script lang="ts">
  let clazz;
  export { clazz as class };
</script>

<style lang="postcss">
  /* noinspection CssUnusedSymbol */
  .card {
    background: rgba(255, 255, 255, 0.2);
    backdrop-filter: blur(10px);
    cursor: pointer;
    user-select: none;
  }

  /* noinspection CssUnusedSymbol */
  .card:active {
    background: rgba(255, 255, 255, 0.35);
  }
</style>
