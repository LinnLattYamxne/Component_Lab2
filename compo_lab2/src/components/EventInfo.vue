<script setup lang="ts">
import type { Event } from '@/types'

defineProps<{
  event: Event
}>()
</script>

<template>
  <div class="event-info-block">
    <p class="right-text">{{ event.category }}</p>
    <p class="right-text">Organized by: {{ event.organizer }}</p>
  </div>
</template>

<style scoped>
.event-info-block {
  width: 250px; /* Matches the width of your EventCard */
}

.right-text {
  text-align: right;
  font-size: 0.9rem; /* Both lines will share this exact same size */
  margin: 2px 0;
}
</style>