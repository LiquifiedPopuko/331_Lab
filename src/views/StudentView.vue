<script setup lang="ts">
import StudentCard from '../components/StudentCard.vue'
import StudentService from '@/services/StudentService'
import { ref, type Ref } from 'vue'
import type { StudentItem } from '@/type';
const students: Ref<Array<StudentItem>> = ref([])
StudentService.getEvent().then((response) => {
  students.value = response.data
})
</script>

<template>
  <h1>Students</h1>
  <main class="students">
    <StudentCard v-for="student in students" :key="student.id" :student="student"></StudentCard>
  </main>
</template>

<style scoped>
.students {
  display: flex;
  flex-direction: column;
  align-items: center;
}

</style>