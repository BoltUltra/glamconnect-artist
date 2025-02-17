<script setup lang="ts"></script>

<template>
  <section
    class="bg-orange-50 md:pt-0 pt-20 dark:bg-gray-600 md:h-auto items-center justify-center grid md:grid-cols-6 mg:gap-0 gap-10 rounded-2xl overflow-hidden my-10 md:px-0 px-5 md:mx-20 transition__custom"
  >
    <div class="max-w-2xl mx-auto md:col-span-4 md:text-left text-center">
      <h1
        class="md:text-8xl text-5xl font-extralight text-gray-900 dark:text-white animate-fade-in"
      >
        Your Beauty, Your Way
      </h1>
      <p class="mt-4 text-gray-700 dark:text-white">
        Find top-rated makeup artist and book beauty services effortlessly,
        whenever and wherever you need them
      </p>
      <div class="mt-6 flex md:flex-row flex-col justify-center gap-5">
        <div
          class="flex items-center space-x-2 bg-white w-full px-3 py-2 rounded-2xl"
        >
          <img src="/images/search-icon.svg" alt="" />
          <input
            type="text"
            placeholder="Explore makeup artist around you"
            class="p-2 w-full"
          />
        </div>
        <button
          class="bg-orange-500 text-white px-16 py-3 rounded-2xl hover:bg-orange-600"
        >
          Search
        </button>
      </div>
    </div>

    <div class="md:col-span-2">
      <img src="/images/hero-img.webp" alt="" />
    </div>
  </section>
</template>

<style scoped></style>
