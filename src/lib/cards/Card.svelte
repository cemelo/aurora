<div class={`card rounded-md flex flex-col ${clazz || ''}`}>
  <slot />
</div>

<script lang="ts">
  let clazz;
  export { clazz as class };
</script>

<style lang="postcss">
  .card {
    background: rgba(255, 255, 255, 0.2);
    border: 2px solid rgba(255, 255, 255, 0.5);
  }
</style>
