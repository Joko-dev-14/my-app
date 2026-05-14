<script setup lang="ts">
import type { FinancialApp } from '../data/mockData'

const props = defineProps<{
  app: FinancialApp
  isLiked: boolean
}>()

const emit = defineEmits<{
  'toggle-like': [id: number]
}>()

const appIcons = import.meta.glob('../assets/app-*.svg',
  {
    eager: true,
    query: 'url',
    import: 'default'
  }) as Record<string, string>

const getAppIcon = (app: FinancialApp) => {
  const key = `../assets/app-${app.id}.svg`
  return appIcons[key] || ''
}

const logoBg: Record<FinancialApp['category'], string> = {
  Investment: 'bg-gradient-to-r from-indigo-50 to-indigo-100',
  Banking: 'bg-gradient-to-r from-emerald-50 to-emerald-100',
  Lending: 'bg-gradient-to-r from-violet-50 to-violet-100',
  Insurance: 'bg-gradient-to-r from-rose-50 to-rose-100',
  Crypto: 'bg-gradient-to-r from-amber-50 to-amber-100',
}

const badgeStyle: Record<FinancialApp['category'], string> = {
  Investment: 'bg-blue-100 text-blue-700',
  Banking: 'bg-teal-100 text-teal-700',
  Lending: 'bg-purple-100 text-purple-700',
  Insurance: 'bg-red-100 text-red-700',
  Crypto: 'bg-orange-100 text-orange-700',
}

function formatDownloads(n: number): string {
  if (n >= 1_000_000) return `${(n / 1_000_000).toFixed(1)}M`
  return `${Math.round(n / 1_000)}K`
}
</script>

<template>
  <!-- Card Container -->
  <div
    class="bg-white rounded-2xl shadow-sm border border-gray-300 overflow-hidden flex flex-col hover:shadow-lg hover:-translate-y-1 transition-all duration-200">

    <!-- Logo -->
    <div :class="['h-36 flex items-center justify-center flex-shrink-0', logoBg[app.category]]">
      <div class="w-16 h-16 bg-white rounded-2xl shadow-md flex items-center justify-center p-1.5">
        <img :src="getAppIcon(app)" :alt="app.name + ' icon'" class="w-full h-full object-contain" />
      </div>
    </div>

    <!-- Card -->
    <div class="p-4 flex flex-col gap-2 flex-1">

      <!-- Category -->
      <div class="flex items-start justify-between gap-2">
        <h3 class="font-semibold text-gray-900 text-sm leading-tight">{{ app.name }}</h3>
        <button @click="emit('toggle-like', app.id)" class="flex-shrink-0 mt-0.5 transition-colors"
          :class="isLiked ? 'text-red-500' : 'text-gray-300 hover:text-gray-400'">
          <span class="material-icons text-[1.1rem]">{{ isLiked ? 'favorite' : 'favorite_border' }}</span>
        </button>
      </div>

      <!-- Category badge -->
      <span
        :class="['text-xs font-semibold px-2 py-0.5 rounded-full w-fit tracking-wide', badgeStyle[app.category]]">
        {{ app.category.toUpperCase() }}
      </span>

      <!-- Category description -->
      <p class="text-gray-500 text-xs leading-relaxed line-clamp-2 flex-1">
        {{ app.description }}
      </p>

      <hr class="border-gray-100 my-1" />

      <!-- Rating + downloads -->
      <div class="flex items-center justify-between mt-auto">

        <!-- Stars + rating -->
        <div class="flex items-center gap-1">
          <div class="flex items-center gap-0">
            <template v-for="i in 5" :key="i">
              <!-- Full star -->
              <svg v-if="app.rating >= i" class="w-4 h-4 text-yellow-400" fill="currentColor" viewBox="0 0 24 24">
                <path
                  d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z" />
              </svg>
              <!-- Half star -->
              <span v-else-if="app.rating >= i - 0.5" class="relative inline-flex w-4 h-4">
                <svg class="absolute w-4 h-4 text-yellow-400" viewBox="0 0 24 24" overflow="hidden">
                  <defs>
                    <clipPath :id="`half-clip-${app.id}-${i}`">
                      <path
                        d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z" />
                    </clipPath>
                  </defs>
                  <path :clip-path="`url(#half-clip-${app.id}-${i})`"
                    d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"
                    fill="none" stroke="currentColor" stroke-width="3" />
                </svg>
                <span class="absolute inset-0 overflow-hidden" style="width: 54%">
                  <svg class="w-4 h-4 text-yellow-400" fill="currentColor" viewBox="0 0 24 24">
                    <path
                      d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z" />
                  </svg>
                </span>
              </span>
              <!-- Empty star -->
              <svg v-else class="w-4 h-4 text-yellow-400" viewBox="0 0 24 24" overflow="hidden">
                <defs>
                  <clipPath :id="`empty-clip-${app.id}-${i}`">
                    <path
                      d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z" />
                  </clipPath>
                </defs>
                <path :clip-path="`url(#empty-clip-${app.id}-${i})`"
                  d="M12 2l3.09 6.26L22 9.27l-5 4.87 1.18 6.88L12 17.77l-6.18 3.25L7 14.14 2 9.27l6.91-1.01L12 2z"
                  fill="none" stroke="currentColor" stroke-width="3" />
              </svg>
            </template>
          </div>
          <span class="text-xs font-medium text-gray-500"> {{ app.rating.toFixed(1) }}</span>
        </div>

        <!-- Downloads -->
        <div class="flex items-center gap-1 text-gray-400">
          <span class="material-icons text-[1.1rem]">cloud_download</span>
          <span class="text-xs text-gray-500"> {{ formatDownloads(app.downloads) }}</span>
        </div>

      </div>
    </div>
  </div>
</template>
