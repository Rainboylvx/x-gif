<template>
  <div id="app">
      <xgif autoload src="/a.gif"></xgif>
  </div>
</template>

<script>
import xgif from './xgif.vue'
export default {
  name: 'app',
  components: {
      xgif
  }
}
</script>

<style>
</style>
