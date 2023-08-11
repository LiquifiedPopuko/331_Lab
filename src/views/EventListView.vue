<script setup lang="ts">
import EventCard from '../components/EventCard.vue'
import EventService from '@/services/EventService'
import { useRouter, onBeforeRouteUpdate } from 'vue-router'
import { ref, type Ref, computed } from 'vue'
import type { EventItem } from '@/type'
import type { AxiosResponse } from 'axios'
const totalEvent = ref<number>(0)
const selectSize = ref<number>(0)
const events: Ref<Array<EventItem>> = ref([])
const router = useRouter()
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
EventService.getEvent(3, props.page)
  .then((response: AxiosResponse<EventItem[]>) => {
    events.value = response.data
    totalEvent.value = response.headers['x-total-count']
  })
  .catch(() => {
    router.push({ name: 'NetworkError' })
  })
onBeforeRouteUpdate((to, from, next) => {
  const toPage = Number(to.query.page)
  EventService.getEvent(3, toPage)
    .then((response: AxiosResponse<EventItem[]>) => {
      events.value = response.data
      totalEvent.value = response.headers['x-total-count']
      next()
    })
    .catch(() => {
      next({ name: 'NetworkError' })
    })
})
const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvent.value / 3)// selectsize.value
  return props.page.valueOf() < totalPages
})
</script>

<template>
  <h1>Events For Good</h1>
  <main class="flex flex-col items-center">
    <EventCard v-for="event in events" :key="event.id" :event="event"></EventCard>
    <div class="flex-auto w-1/6">
      <div class="text-left">
      <RouterLink
        :to="{ name: 'EventList', query: { page: page - 1, size: selectSize } }"
        rel="prev"
        v-if="page != 1"
        >Prev Page</RouterLink
      ></div>
      <div class="text-right">
      <RouterLink
        :to="{ name: 'EventList', query: { page: page + 1, size: selectSize } }"
        rel="next"
        v-if="hasNextPage"
        >Next Page</RouterLink>
      </div>
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