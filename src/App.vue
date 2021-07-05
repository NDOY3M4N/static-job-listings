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
            <InputTag
              :categories="categoriesToFilter"
              @remove-filter="removeFilter"
              @remove-all-filters="removeAllFilter"/>
          </div>
        </transition>
        <!-- Jobs -->
        <ul class="py-20 space-y-14 sm:space-y-10">
          <transition-group
            enter-active-class="transform transition duration-700 ease-in-out"
            enter-from-class="opacity-0 scale-75"
            enter-to-class="opacity-100 scale-100"
            leave-from-class="opacity-100 scale-100"
            leave-to-class="opacity-0 scale-75"
            leave-active-class="transform transition duration-700 ease-in-out">
            <JobCard
              v-for="job in jobsFiltered" :key="job.id"
              class="transition duration-500 ease-in-out"
              :job="job" @add-filter="addFilter" />
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
import InputTag from './components/InputTag.vue'
import JobCard from './components/JobCard.vue'

export default {
  components: { InputTag, JobCard },
  setup() {
    const jobs = ref(data)

    const categoriesToFilter = ref([])

    const addFilter = (category) => {
      if (categoriesToFilter.value.indexOf(category) < 0) {
        categoriesToFilter.value.push(category)
      }
    }

    const removeFilter = (category) => {
      const categoryIndex = categoriesToFilter.value.indexOf(category)

      categoriesToFilter.value.splice(categoryIndex, 1)
    }

    const removeAllFilter = () => {
      categoriesToFilter.value = []
    }

    const jobsFiltered = computed(() => {
      if (categoriesToFilter.value.length === 0) return jobs.value

      return jobs.value.filter(job => {
        let match = true
        const jobCategories = [job.languages, job.role, job.level, job.tools].flat()

        categoriesToFilter.value.forEach(categorie => {
          match = match && (jobCategories.indexOf(categorie) >= 0)
        })

        return match
      })
    })

    return { categoriesToFilter, addFilter, removeFilter, removeAllFilter, jobsFiltered }
  }
}
</script>
