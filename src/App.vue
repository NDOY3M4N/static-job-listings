<template>
  <div class="min-h-screen flex flex-col">
    <header class="bg-primary h-40">
      <picture>
        <source media="(min-width: 650px)" srcset="./assets/bg-header-desktop.svg" />
        <img class="w-full h-full object-cover" src="./assets/bg-header-mobile.svg" alt="Background header">
      </picture>
    </header>
    <div class="bg-neutral-100 flex-1">
      <main class="container mx-auto px-8">
        <!-- filter -->
        <div class="-mt-10" v-show="true">
          <div class="p-5 flex items-center justify-between bg-white rounded-md shadow-lg">
            <div class="flex-1 flex items-center gap-4 flex-wrap">
              <div v-for="i in 4" :key="i" class="flex rounded overflow-hidden">
                <span class="p-2 bg-neutral-200 text-primary text-xs font-bold">FrontEnd</span>
                <button aria-label="Remove Tag" class="p-2 bg-primary transition-colors duration-300 hover:bg-neutral-400">
                  <img src="./assets/icon-remove.svg" alt="Remove tag">
                </button>
              </div>
            </div>
            <div class="flex-none">
              <button class="px-3 py-2 text-sm font-bold text-neutral-300 hover:underline hover:text-primary">Clear</button>
            </div>
          </div>
        </div>
        <!-- Jobs -->
        <div class="py-20 space-y-12">
          <div v-for="i in 5" :key="i" class="relative p-6 bg-white rounded-md shadow-lg border-l-4 border-primary divide-y sm:px-10 sm:py-8 lg:divide-y-0 lg:flex lg:items-center lg:justify-between">
            <div class="pb-4 sm:flex sm:items-center sm:flex-1 lg:pb-0">
              <div class="absolute top-0 left-5 transform -translate-y-1/2 sm:static sm:translate-y-0 sm:flex-none">
                <img src="./assets/photosnap.svg" alt="Photosnap" class="w-16 h-auto object-cover sm:w-24 sm:h-auto">
              </div>
              <div class="mt-4 space-y-3 sm:mt-0 sm:ml-6">
                <div class="inline-flex items-center space-x-3">
                  <h1 class="text-primary text-sm font-bold">Photosnap</h1>
                  <span class="py-1 px-2 bg-primary rounded-full text-white text-xs font-bold uppercase inline-block">New!</span>
                  <span class="py-1 px-2 bg-black rounded-full text-white text-xs font-bold uppercase inline-block">Featured</span>
                </div>
                <h2 class="text-neutral-400 text-md font-bold transition-colors duration-300 hover:text-primary">Senior Frontend Developer</h2>
                <div class="text-neutral-300 text-sm inline-flex items-center space-x-2">
                  <span>1d ago</span>
                  <span class="text-2xl">&bull;</span>
                  <span>Full Time</span>
                  <span class="text-2xl">&bull;</span>
                  <span>USA only</span>
                </div>
              </div>
            </div>

            <div class="pt-5 flex items-center gap-4 flex-wrap lg:pt-0 lg:flex-none">
              <button v-for="i in 5" :key="i" class="p-2 bg-neutral-200 text-primary text-xs font-bold rounded transition-colors duration-300 hover:bg-primary hover:text-white">
                Frontend
              </button>
            </div>
          </div>
        </div>
      </main>

      <footer class="pb-10 text-center text-sm text-neutral-400">
        Challenge by <a class="underline text-primary font-bold" rel="noopener" href="https://www.frontendmentor.io?ref=challenge" target="_blank">Frontend Mentor</a>. 
        Coded by <a class="underline text-primary font-bold" rel="noopener" href="https://github.com/NDOY3M4N">Abdoulaye NDOYE</a>.
      </footer>
    </div>
  </div>
</template>