<script setup lang="ts">
import EventCard from '../components/EventCard.vue'
import EventService from '@/services/EventService'
import { ref, type Ref, watchEffect, computed } from 'vue'
import type { EventItem } from '@/type';
import type { AxiosResponse } from 'axios';
const totalEvent = ref<number>(0)
const selectSize = ref<number>(0)
const events: Ref<Array<EventItem>> = ref([])
const props = defineProps({
  size: {
    type: Number,
    required: true
  },
  page: {
    type: Number,
    required: true
  }
})
watchEffect (() => {
  EventService.getEvent(selectSize.value, props.page).then((response: AxiosResponse<EventItem[]>) => {
    events.value = response.data
    totalEvent.value = response.headers['x-total-count']
  })
})
const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvent.value/selectSize.value)
  return props.page.valueOf() < totalPages
})
</script>

<template>
  <h1>Events For Good</h1>
  <main class="events">
    <EventCard v-for="event in events" :key="event.id" :event="event"></EventCard>
    <div class="pagination">
      <RouterLink :to="{name: 'EventList', query: {page: page - 1, size: selectSize}}" rel="prev" v-if="page != 1" id="page-prev">Prev Page</RouterLink>
      <RouterLink :to="{name: 'EventList', query: {page: page + 1, size: selectSize}}" rel="next" v-if="hasNextPage" id="page-next">Next Page</RouterLink>
    </div>
    <select name="selectSize" v-model="selectSize">
      <option value="1">1</option>
      <option value="2" selected>2</option>
      <option value="3">3</option>
      <option value="4">4</option>
      <option value="5">5</option>
      <option value="6">6</option>
    </select>
    </main>
</template>

<style scoped>
.events {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.pagination {
  display: flex;
  width: 290px;
}
.pagination a {
  flex: 1;
  text-decoration: none;
  columns: #2c3e50;
}

#page-prev {
  text-align: left;
}

#page-next {
  text-align: right;
}
</style>