<template>
  <button type="button" class="btn" :class="active ? '' : 'disabled'" :style="{ color: color }">
    <i :class="iconClass"></i>
  </button>
</template>

<script>
export default {
  name: 'Button',
  props: {
    iconClass: String,
    color: String,
    active: Boolean
  }
}
</script>

<style>

</style>