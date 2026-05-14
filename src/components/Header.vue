<template>
  <header class="bg-white border-b border-gray-200 sticky top-0 z-30 shadow-sm">
    <div class="flex items-center justify-between px-4 md:px-6 h-[5.5rem] gap-4">

      <!-- Logo + Title -->
      <div class="flex items-center gap-3 flex-shrink-0">
        <div class="w-9 h-9 bg-indigo-600 rounded-xl flex items-center justify-center flex-shrink-0">
          <span class="material-icons text-white text-[1.25rem]">storefront</span>
        </div>
        <div class="hidden sm:block">
          <h1 class="text-base font-bold text-gray-900 leading-tight">Financial App Store</h1>
          <p class="text-xs text-gray-500">Discover the best financial tools for your needs</p>
        </div>
        <h1 class="sm:hidden text-sm font-bold text-gray-900">Financial App Store</h1>
      </div>

      <!-- Search -->
      <div class="flex-1 max-w-xs md:max-w-sm">
        <div class="relative">
          <span
            class="material-icons absolute left-4 top-1/2 -translate-y-1/2 text-gray-400 text-[1.1rem] pointer-events-none">search</span>
          <input type="text" placeholder="Search apps..."
            class="w-full pl-10 pr-8 py-3.5 bg-gray-100 rounded-lg text-sm text-gray-800 placeholder-gray-400 focus:outline-none focus:ring-2 focus:ring-indigo-300 focus:bg-white transition" />
        </div>
      </div>

    </div>
  </header>
</template>
