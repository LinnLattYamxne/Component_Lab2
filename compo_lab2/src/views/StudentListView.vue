<script setup lang="ts">
import { ref, onMounted } from 'vue'
import type { Student } from '@/types'
import StudentService from '@/services/StudentService'

const students = ref<Student[] | null>(null)

onMounted(() => {
  StudentService.getStudents()
    .then((response) => {
      students.value = response.data
    })
    .catch((error) => {
      console.error('Error fetching students:', error)
    })
})
</script>

<template>
  <h1>Student Directory</h1>
  
  <div class="student-list" v-if="students">
    <div v-for="student in students" :key="student.id" class="student-card">
      <h2>{{ student.name }} {{ student.surname }}</h2>
      <p><strong>Student ID:</strong> {{ student.studentId }}</p>
      <p class="gpa"><strong>GPA:</strong> {{ student.gpa }}</p>
    </div>
  </div>
</template>

<style scoped>
.student-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.student-card {
  border: 1px solid #2c3e50;
  padding: 20px;
  width: 300px;
  margin-bottom: 18px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  text-align: left;
}

.student-card h2 {
  margin: 0 0 10px 0;
  font-size: 1.4rem;
  color: #42b983;
}

.gpa {
  color: #e74c3c;
  font-weight: bold;
}
</style>