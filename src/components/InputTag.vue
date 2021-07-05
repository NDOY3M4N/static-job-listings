<template>
  <div class="p-5 flex items-center justify-between bg-white rounded-md shadow-lg">
    <div class="flex-1 flex items-center gap-4 flex-wrap">
      <div v-for="category in categories" :key="category" class="flex rounded overflow-hidden">
        <span class="p-2 bg-neutral-200 text-primary text-xs font-bold">{{ category }}</span>
        <button @click="$emit('remove-filter', category)" aria-label="Remove Tag" class="p-2 bg-primary transition-colors duration-300 hover:bg-neutral-400">
          <img src="/images/icon-remove.svg" alt="Remove tag">
        </button>
      </div>
    </div>
    <div class="flex-none">
      <button
        @click="$emit('remove-all-filters')"
        class="px-3 py-2 text-sm font-bold text-neutral-300 hover:underline hover:text-primary">Clear</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    categories: Array
  }
}
</script>
