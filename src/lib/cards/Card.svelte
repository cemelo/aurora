<div class={`card rounded-md flex flex-col ${clazz || ''}`}>
  <div class="controls grow">
    <slot name="controls" />
  </div>
  <div class="info h-2/5">
    <slot name="info" />
  </div>
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

  .card .info {
    background: rgba(255, 255, 255, 0.2);
  }
</style>
