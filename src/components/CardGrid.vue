<script setup lang="ts">
import type { FinancialApp } from '../data/mockData'
import Card from './Card.vue'

const props = defineProps<{
  apps: FinancialApp[]
  totalApps: number
  sortBy: string
  likedAppIds: Set<number>
}>()

const emit = defineEmits<{
  'toggle-like': [id: number]
  'change-sort': [sortBy: string]
}>()
</script>

<template>
  <div>
    <!-- Toolbar -->
    <div class="flex items-center justify-between mb-5">
      <p class="text-sm text-gray-600">
        Showing <span class="font-semibold text-gray-900">11</span> of
        <span class="font-semibold text-gray-900">48</span> apps
      </p>

      <div
        class="flex items-center gap-2 border border-gray-200 rounded-lg px-3 py-2.5 bg-white text-sm text-gray-700 shadow-sm">
        <span class="material-icons text-gray-400 text-[1.1rem]">sort</span>
        <span class="font-light">Sort: Top Rated</span>
        <span class="material-icons text-gray-400 text-[1.1rem]">keyboard_arrow_down</span>
      </div>
    </div>

    <!-- Cards Grid -->
    <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-5">
      <!-- Cards go here -->
      <Card v-for="app in apps" :key="app.id" :app="app" :is-liked="likedAppIds.has(app.id)"
        @toggle-like="emit('toggle-like', $event)" />
    </div>
  </div>
</template>
