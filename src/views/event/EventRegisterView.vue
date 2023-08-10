<script setup lang="ts">
import type { EventItem } from '@/type'
import type { PropType } from 'vue';
import { useMessageStore } from '@/stores/message';
import { useRouter } from 'vue-router'
const props = defineProps({
    event: {
        type: Object as PropType<EventItem>,
        require: true
    }
})
const store = useMessageStore()
const router = useRouter()
function register() {
    store.updateMessage('You are successfully registered for ' + props.event?.title)
    setTimeout(() => {
        store.resetMessage()
    }, 3000)
    router.push({
        name: 'event-detail',
        params: {
            id: props.event?.id
        }
    })
}
</script>

<template>
    <p>Registration from here</p>
    <button @click="register">Register Me</button>
</template>