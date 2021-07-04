<template>
  <div class="min-h-screen flex flex-col">
    <header class="bg-primary h-40">
      <picture>
        <source media="(min-width: 650px)" srcset="/images/bg-header-desktop.svg" />
        <img class="w-full h-full object-cover" src="/images/bg-header-mobile.svg" alt="Background header">
      </picture>
    </header>
    <div class="bg-neutral-100 flex-1">
      <main class="max-w-xl mx-auto px-4 sm:px-8 md:max-w-3xl lg:max-w-6xl md:px-12 2xl:max-w-7xl">
        <!-- filter -->
        <transition
          enter-active-class="transform transition duration-500 ease-in-out"
          enter-from-class="opacity-0 -translate-y-2"
          enter-to-class="opacity-100 translate-y-0"
          leave-active-class="transform transition duration-500 ease-in-out"
          leave-from-class="opacity-100 translate-y-0"
          leave-to-class="opacity-0 -translate-y-2">
          <div class="-mt-10" v-show="categoriesToFilter.length > 0">
            <div class="p-5 flex items-center justify-between bg-white rounded-md shadow-lg">
              <div class="flex-1 flex items-center gap-4 flex-wrap">
                <div v-for="category in categoriesToFilter" :key="category" class="flex rounded overflow-hidden">
                  <span class="p-2 bg-neutral-200 text-primary text-xs font-bold">{{ category }}</span>
                  <button @click="removeFilter(category)" aria-label="Remove Tag" class="p-2 bg-primary transition-colors duration-300 hover:bg-neutral-400">
                    <img src="/images/icon-remove.svg" alt="Remove tag">
                  </button>
                </div>
              </div>
              <div class="flex-none">
                <button @click="removeAllFilter" class="px-3 py-2 text-sm font-bold text-neutral-300 hover:underline hover:text-primary">Clear</button>
              </div>
            </div>
          </div>
        </transition>
        <!-- Jobs -->
        <ul class="py-20 space-y-14 sm:space-y-10">
          <transition-group
            enter-active-class="transform transition duration-500 ease-in-out"
            enter-from-class="opacity-0 -translate-x-5"
            enter-to-class="opacity-100 translate-x-0"
            leave-from-class="opacity-100 translate-x-0"
            leave-to-class="opacity-0 -translate-x-5"
            leave-active-class="transform transition duration-500 ease-in-out">
            <li v-for="job in jobsFiltered" :key="job.id"
              class="relative p-6 bg-white rounded-md shadow-lg divide-y sm:px-10 sm:py-8 lg:divide-y-0 lg:flex lg:items-center lg:justify-between"
              :class="{'border-l-5 border-primary': job.featured }">
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
                <button v-for="category in categorize(job.id)" :key="category"
                  @click="addFilter(category)"
                  class="p-2 bg-neutral-200 text-primary text-xs font-bold rounded transition-colors duration-300 hover:bg-primary hover:text-white">
                  {{ category }}
                </button>
              </div>
            </li>
          </transition-group>
        </ul>
      </main>

      <footer class="pb-10 text-center text-sm text-neutral-400">
        Challenge by <a class="underline text-primary font-bold" rel="noopener" href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>. 
        Coded by <a class="underline text-primary font-bold" rel="noopener" href="https://github.com/NDOY3M4N">Abdoulaye NDOYE</a>.
      </footer>
    </div>
  </div>
</template>

<script>
import { ref, computed } from 'vue'
import data from './data'

export default {
  setup() {
    const jobs = ref(data)

    const categorize = (jobId) => {
      const jobToCategorize = jobs.value.find(job => job.id === jobId)

      return [jobToCategorize.role, jobToCategorize.level, jobToCategorize.languages, jobToCategorize.tools].flat()
    }

    const categoriesToFilter = ref([])

    const addFilter = (category) => {
      const categoryExists = categoriesToFilter.value.find(cat => cat === category)
      if (categoryExists) return

      categoriesToFilter.value.push(category)
      jobsFiltered.value = categoriesToFilter.value
    }

    const removeFilter = (category) => {
      const categoryIndex = categoriesToFilter.value.findIndex(cat => cat === category)

      categoriesToFilter.value.splice(categoryIndex, 1)
      jobs.value = data
      jobsFiltered.value = categoriesToFilter.value
    }

    const removeAllFilter = () => {
      categoriesToFilter.value = []

      jobs.value = data
    }

    const jobsFiltered = computed({
      get: () => jobs.value,
      set: categories => {
        categories.forEach(categorie => {
          jobs.value = jobs.value.filter(job => {
            const CONDITION_1 = job.role === categorie
            const CONDITION_2 = job.level === categorie
            const CONDITION_3 = job.languages.find(lang => lang === categorie)
            const CONDITION_4 = job.tools.find(tool => tool === categorie)
  
            if (CONDITION_1 || CONDITION_2 || CONDITION_3 || CONDITION_4) {
              return job
            }
          })
        })
      }
    })

    return { jobs, categorize, categoriesToFilter, addFilter, removeFilter, removeAllFilter, jobsFiltered }
  }
}
</script>
