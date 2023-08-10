<script setup lang="ts">
import type { EventItem } from '@/type'
import type { PropType } from 'vue';
import { useMessageStore } from '@/stores/message';
import { useRouter } from 'vue-router';
const props = defineProps({
    event: {
        type: Object as PropType<EventItem>,
        require: true
    }
})
const store = useMessageStore()
const router = useRouter()
function edit() {
    router.push({
        name: 'event-detail',
        params: {
            id: props.event?.id
        }
    })
    store.updateMessage('The data have been updated')
    setTimeout(() => {
        store.resetMessage()
    }, 3000)
}
</script>

<template>
    <p>Edit the event here</p>
    <button @click="edit">Edit</button>
</template>