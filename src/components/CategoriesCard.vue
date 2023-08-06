<template>
  <div class="category-card">
    <p>{{ event?.category }}</p>
    <p>{{ event?.organizer }}</p>
  </div>
</template>

<script setup lang="ts">
import type { EventItem } from '@/type'
import type { PropType } from 'vue'
const props = defineProps({
  event: {
    type: Object as PropType<EventItem>,
    require: true
  }
})
</script>

<style scoped>
.category-card {
  width: auto;
  cursor: pointer;
  margin-bottom: 18px;
  text-align: end;
}
.category-card:hover {
  transform: scale(1.01);
  box-shadow: 0 3px 12px 0 rgba(0, 0, 0, 0.2);
}
</style>
