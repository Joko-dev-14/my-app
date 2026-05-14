<script setup lang="ts">
defineProps<{
  selectedCategory: string
  minRating: string
  downloadFilter: string
  showLikedOnly: boolean
  hasActiveFilters: boolean
}>()

const emit = defineEmits<{
  'update:selectedCategory': [value: string]
  'update:minRating': [value: string]
  'update:downloadFilter': [value: string]
  'update:showLikedOnly': [value: boolean]
  'clear-filters': []
}>()
</script>

<template>
  <div class="p-5 flex flex-col gap-6 h-full">

    <!-- Active filters -->
    <div>
      <p class="text-xs font-semibold text-gray-500 mb-2">Active filters</p>
      <button @click="emit('clear-filters')" :disabled="!hasActiveFilters"
        class="w-full px-3 py-2 rounded-lg text-sm font-semibold border transition" :class="hasActiveFilters
          ? 'border-indigo-200 text-indigo-600 bg-indigo-50 hover:bg-indigo-100 cursor-pointer'
          : 'border-gray-200 text-gray-400 bg-gray-50 cursor-not-allowed'">
        Clear All Filters
      </button>
    </div>

    <hr class="border-gray-100" />

    <!-- Category -->
    <div>
      <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-2">Category</p>
      <ul class="space-y-0.5">
        <li v-for="cat in ['All Categories', 'Investment', 'Banking', 'Lending', 'Insurance', 'Crypto']" :key="cat">
          <button @click="emit('update:selectedCategory', cat)"
            class="w-full text-left px-3 py-1.5 rounded-lg text-sm transition" :class="selectedCategory === cat
              ? 'text-indigo-600 font-semibold bg-indigo-50 border-l-2 border-indigo-600'
              : 'text-gray-700 hover:bg-gray-50'">
            {{ cat }}
          </button>
        </li>
      </ul>
    </div>

    <!-- Min Rating -->
    <div>
      <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-2">Min Rating</p>
      <ul class="space-y-0.5">
        <li v-for="opt in ['All', '4+', '3+', '2+']" :key="opt">
          <button @click="emit('update:minRating', opt)"
            class="w-full text-left px-3 py-1.5 rounded-lg text-sm transition flex items-center gap-2" :class="minRating === opt
              ? 'text-indigo-600 font-semibold bg-indigo-50 border-l-2 border-indigo-600'
              : 'text-gray-700 hover:bg-gray-50'">
            <span v-if="opt !== 'All'" class="text-yellow-400 text-xs">★</span>
            {{ opt }}
          </button>
        </li>
      </ul>
    </div>

    <!-- Liked -->
    <div>
      <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-2">Liked</p>
      <button @click="emit('update:showLikedOnly', !showLikedOnly)"
        class="w-full text-left px-3 py-1.5 rounded-lg text-sm transition flex items-center gap-2" :class="showLikedOnly
          ? 'text-indigo-600 font-semibold bg-indigo-50 border-l-2 border-indigo-600'
          : 'text-gray-700 hover:bg-gray-50'">
        <span class="material-icons text-[1rem]" :class="showLikedOnly ? 'text-red-500' : 'text-gray-300'">{{
          showLikedOnly ? 'favorite' : 'favorite_border' }}</span>
        Show liked apps
      </button>
    </div>

    <!-- Downloads -->
    <div>
      <p class="text-xs font-semibold text-gray-400 uppercase tracking-wider mb-2">Downloads</p>
      <ul class="space-y-0.5">
        <li v-for="opt in ['All', 'High (1M+)', 'Medium (100K+)', 'Low']" :key="opt">
          <button @click="emit('update:downloadFilter', opt)"
            class="w-full text-left px-3 py-1.5 rounded-lg text-sm transition" :class="downloadFilter === opt
              ? 'text-indigo-600 font-semibold bg-indigo-50 border-l-2 border-indigo-600'
              : 'text-gray-700 hover:bg-gray-50'">
            {{ opt }}
          </button>
        </li>
      </ul>
    </div>

  </div>
</template>
