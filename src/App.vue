<script setup lang="ts">
import { ref, computed } from 'vue'
import { mockApps } from './data/mockData'
import Header from './components/Header.vue'
import Sidebar from './components/Sidebar.vue'
import CardGrid from './components/CardGrid.vue'

// Filter state
const selectedCategory = ref('All Categories')
const minRating = ref('All')
const downloadFilter = ref('All')
const showLikedOnly = ref(false)
const likedAppIds = ref(new Set<number>())
const sortBy = ref('Top Rated')

// Filtered + sorted apps
const filteredApps = computed(() => {
  let apps = mockApps.filter(app => {
    if (selectedCategory.value !== 'All Categories' && app.category !== selectedCategory.value) return false
    const minR = minRating.value === '4+' ? 4 : minRating.value === '3+' ? 3 : minRating.value === '2+' ? 2 : 0
    if (app.rating < minR) return false
    if (downloadFilter.value === 'High (1M+)' && app.downloads < 1_000_000) return false
    if (downloadFilter.value === 'Medium (100K+)' && (app.downloads < 100_000 || app.downloads >= 1_000_000)) return false
    if (downloadFilter.value === 'Low' && app.downloads >= 100_000) return false
    if (showLikedOnly.value && !likedAppIds.value.has(app.id)) return false
    return true
  })

  if (sortBy.value === 'Top Rated') return [...apps].sort((a, b) => b.rating - a.rating)
  if (sortBy.value === 'Most Downloads') return [...apps].sort((a, b) => b.downloads - a.downloads)
  if (sortBy.value === 'A-Z') return [...apps].sort((a, b) => a.name.localeCompare(b.name))
  return apps
})

const hasActiveFilters = computed(() =>
  selectedCategory.value !== 'All Categories' ||
  minRating.value !== 'All' ||
  downloadFilter.value !== 'All' ||
  showLikedOnly.value
)

function clearFilters() {
  selectedCategory.value = 'All Categories'
  minRating.value = 'All'
  downloadFilter.value = 'All'
  showLikedOnly.value = false
}

function toggleLike(appId: number) {
  const next = new Set(likedAppIds.value)
  if (next.has(appId)) next.delete(appId)
  else next.add(appId)
  likedAppIds.value = next
}
</script>

<template>
  <div class="h-screen overflow-hidden bg-gray-50 flex flex-col">
    <Header />

    <div class="flex flex-1 overflow-hidden">

      <!-- Sidebar -->
      <aside class="hidden md:block w-60 bg-white border-r border-gray-200 overflow-y-auto flex-shrink-0">
        <Sidebar :selected-category="selectedCategory" :min-rating="minRating" :download-filter="downloadFilter"
          :show-liked-only="showLikedOnly" :has-active-filters="hasActiveFilters"
          @update:selected-category="selectedCategory = $event" @update:min-rating="minRating = $event"
          @update:download-filter="downloadFilter = $event" @update:show-liked-only="showLikedOnly = $event"
          @clear-filters="clearFilters" />
      </aside>

      <!-- Main content -->
      <main class="flex-1 min-w-0 overflow-y-auto p-4 md:p-6">
        <CardGrid :apps="filteredApps" :total-apps="mockApps.length" :sort-by="sortBy" :liked-app-ids="likedAppIds"
          @toggle-like="toggleLike" @change-sort="sortBy = $event" />
      </main>
    </div>
  </div>
</template>
