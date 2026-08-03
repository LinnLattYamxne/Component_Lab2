<script setup lang="ts">
import EventCard from '@/components/EventCard.vue'
// import EventInfo from '@/components/EventInfo.vue'
import type { Event } from '@/types'
import { ref, onMounted, computed, watchEffect } from 'vue'
import EventService from '@/services/EventService.ts'
import { useRouter } from 'vue-router'

const router = useRouter()

const events = ref<Event[] | null>(null)
const totalEvents = ref<number>(0)
const hasNextPage = computed(() => {
  const totalPages = Math.ceil(totalEvents.value / 3)
  return page.value < totalPages
})

const props = defineProps({
  page: {
    type: Number,
    required: true
  },
  size: {
    type: Number,
    default: 2
  }
})

const page = computed(() => props.page)
const size = computed(() => props.size)

onMounted(() => {
  watchEffect(() => {
    EventService.getEvents(3, page.value)
      .then((response) => {
        events.value = response.data
        totalEvents.value = response.headers['x-total-count']
      })
      .catch(() => {
        router.push({ name: 'network-error-view' })
      })
  })
})
</script>

<template>
  <h1>Events for Good</h1>

  <div class="flex flex-col items-center">
    <EventCard v-for="event in events" :key="event.id" :event="event" />

    <!-- Pagination links -->
    <div class="flex w-[290px]">
      <RouterLink
        id="page-prev"
        class="flex-1 text-left no-underline text-gray-700"
        :to="{ name: 'event-list-view', query: { page: page - 1, size: size } }"
        rel="prev"
        v-if="page != 1"
      >&#60; Prev Page</RouterLink>

      <RouterLink
        id="page-next"
        class="flex-1 text-right no-underline text-gray-700"
        :to="{ name: 'event-list-view', query: { page: page + 1, size: size } }"
        rel="next"
        v-if="hasNextPage"
      >Next Page &#62;</RouterLink>
    </div>

    <!-- Size selector -->
    <div class="mt-5">
      <span>Show per page: </span>
      <RouterLink 
        :class="{ 'font-bold text-green-500': size === 2, 'text-gray-700': size !== 2 }" 
        :to="{ name: 'event-list-view', query: { page: 1, size: 2 } }"
      >2</RouterLink>
      <span class="mx-1">|</span>
      <RouterLink 
        :class="{ 'font-bold text-green-500': size === 4, 'text-gray-700': size !== 4 }" 
        :to="{ name: 'event-list-view', query: { page: 1, size: 4 } }"
      >4</RouterLink>
      <span class="mx-1">|</span>
      <RouterLink 
        :class="{ 'font-bold text-green-500': size === 6, 'text-gray-700': size !== 6 }" 
        :to="{ name: 'event-list-view', query: { page: 1, size: 6 } }"
      >6</RouterLink>
    </div>
  </div>
</template>
