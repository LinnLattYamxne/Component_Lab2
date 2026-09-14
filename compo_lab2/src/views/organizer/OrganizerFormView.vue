<script setup lang="ts">
import OrganizerService from '@/services/OrganizerService'
import { useMessageStore } from '@/stores/message'
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const organizer = ref({
  id: null,
  name: '',
  address: ''
})

const router = useRouter()
const store = useMessageStore()

function saveOrganizer() {
  OrganizerService.saveOrganizer(organizer.value)
    .then((response) => {
      store.updateMessage('Successfully added organization: ' + response.data.name)
      setTimeout(() => {
        store.resetMessage()
      }, 3000)
      router.push({ name: 'event-list-view' })
    })
    .catch(() => {
      router.push({ name: 'network-error-view' })
    })
}
</script>

<template>
  <div>
    <h1>Create an Organization</h1>
    <form @submit.prevent="saveOrganizer">
      <label class="block text-gray-500 font-bold">Organization Name</label>
      <input
        v-model="organizer.name"
        type="text"
        placeholder="Name"
        class="h-13 w-1/4 px-2.5 text-xl border border-gray-400 focus:border-emerald-500 focus:outline-none mb-6"
        required
      />

      <label class="block text-gray-500 font-bold">Address</label>
      <input
        v-model="organizer.address"
        type="text"
        placeholder="Address"
        class="h-13 w-1/4 px-2.5 text-xl border border-gray-400 focus:border-emerald-500 focus:outline-none mb-6"
        required
      />

      <button
        class="flex mx-auto items-center justify-center text-center h-13 px-10 rounded-md font-semibold whitespace-nowrap border border-gray-400 focus:border-emerald-500 transition-all duration-200 ease-linear hover:scale-105 hover:border-emerald-500 hover:shadow-lg active:scale-100 focus:outline-none mb-6"
        type="submit"
      >
        Submit
      </button>
    </form>

    <pre>{{ organizer }}</pre>
  </div>
</template>