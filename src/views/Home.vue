<template>
  <div class="home">
    <h1 class="title">Welcome to Invoicely</h1>
  </div>
  <MapLeaf></MapLeaf>
  <div>

  </div>
</template>

<script>
import MapLeaf from '@/components/MapLeaf.vue'
export default {
  name: 'Home',
  components: {
    MapLeaf
  }
}
</script>
