<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import type { EventItem } from '@/type'
import EventService from '@/services/EventService';
const event = ref<EventItem | null> (null)
const props = defineProps({
    id: String
})
EventService.getEventById(Number(props.id))
.then((response) => {
    event.value = response.data
}).catch(error => {
    console.log(error);
    if (error.response && error.response.status === 404) {
        router.push({ name: '404-resource', params: { resource: 'event'}})
    } else {
        router.push({ name: 'network-error'})
    }
})
const router = useRouter()
</script>

<template>
    <div v-if="event">
        <h1>{{ event?.title }}</h1>
        <RouterLink :to="{name: 'event-detail', params: { id }}">
        Details            
        </RouterLink>|
        <RouterLink :to="{name: 'event-register', params: { id }}">
        Register         
        </RouterLink>|
        <RouterLink :to="{name: 'event-edit', params: { id }}">
        Edit          
        </RouterLink>
        <RouterView :event="event"></RouterView>
    </div>
</template>