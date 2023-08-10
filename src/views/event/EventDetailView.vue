<script setup lang="ts">
import type { EventItem } from '@/type'
import type { PropType } from 'vue';
import { useMessageStore } from '@/stores/message'
import { storeToRefs } from 'pinia';
const store = useMessageStore()
const { message } = storeToRefs(store)
defineProps({
    event: {
        type: Object as PropType<EventItem>,
        require: true
    }
})
</script>

<template>
    <div id="flashMessage" v-if="message">
      <h4>{{ message }}</h4>
    </div>
    <div v-if="event">
        <p>{{ event?.time }} on {{ event?.date }} @ {{ event?.location }}</p>
        <p>{{ event?.description }}</p>
    </div>
</template>