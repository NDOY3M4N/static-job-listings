<template>
  <li
    :class="{'border-l-5 border-primary': job.featured }"
    class="relative p-6 bg-white rounded-md shadow-lg divide-y divide-neutral-300 sm:px-10 sm:py-8 lg:divide-y-0 lg:flex lg:items-center lg:justify-between">
    <div class="pb-4 sm:flex sm:items-center sm:flex-1 lg:pb-0">
      <div class="absolute top-0 left-5 transform -translate-y-1/2 sm:static sm:translate-y-0 sm:flex-none">
        <img :src="job.logo" :alt="job.company"
          class="w-16 h-auto object-cover sm:w-24 sm:h-auto">
      </div>
      <div class="mt-4 space-y-3 sm:mt-0 sm:ml-6">
        <div class="inline-flex items-center space-x-3">
          <h1 class="text-primary text-sm font-bold pt-px">{{ job.company }}</h1>
          <span v-show="job.new" class="py-1.5 px-2.5 bg-primary rounded-full text-white text-xs leading-none font-bold uppercase">New!</span>
          <span v-show="job.featured" class="py-1.5 px-2.5 bg-black rounded-full text-white text-xs leading-none font-bold uppercase">Featured</span>
        </div>
        <h2 class="text-neutral-400 text-md font-bold cursor-pointer transition-colors duration-300 hover:text-primary">{{ job.position }}</h2>
        <div class="text-neutral-300 text-sm inline-flex items-center space-x-1">
          <span>{{ job.postedAt }}</span>
          <span class="text-xl">&bull;</span>
          <span>{{ job.contract }}</span>
          <span class="text-xl">&bull;</span>
          <span>{{ job.location }}</span>
        </div>
      </div>
    </div>

    <div class="pt-5 flex items-center gap-4 flex-wrap lg:pt-0 lg:flex-none">
      <button v-for="category in categories" :key="category"
        @click="$emit('add-filter', category)"
        class="p-2 bg-neutral-200 text-primary text-xs font-bold rounded transition-colors duration-300 hover:bg-primary hover:text-white">
        {{ category }}
      </button>
    </div>
  </li>
</template>

<script>
import { computed } from 'vue'

export default {
  props: {
    job: Object
  },
  setup(props) {
    const categories = computed(() => [props.job.role, props.job.level, props.job.languages, props.job.tools].flat())

    return { categories }
  }
}
</script>
