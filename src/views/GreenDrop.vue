
<template>
  <div id="map">
    <InteractiveMap />
    <!-- <InteractiveMapTest /> -->
  </div>
</template>

<script setup>
import { ref } from 'vue';
import InteractiveMap from '../components/InteractiveMap.vue';

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<style scoped>
.read-the-docs {
  color: #888;
}
</style>
