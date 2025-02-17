<template>
  <Navbar />
  <div class="min-h-screen max-w-[1440px] mx-auto md:px-20 px-5">
    <!-- Search Header -->
    <div class="text-center mb-10 mt-20">
      <h2 class="text-4xl font-light mb-6">Search Result for "KADUNA"</h2>
      <div class="flex md:flex-row flex-col gap-4 max-w-3xl mx-auto w-full">
        <div
          class="flex items-center space-x-2 bg-white w-full px-3 rounded-2xl border md:py-0 py-2"
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
        <button
          class="px-4 md:px-10 py-2 border rounded-lg hover:bg-gray-50 transition-colors flex items-center space-x-2 justify-center w-auto"
        >
          <span>Filter</span>
          <Icon name="gridicons:filter" />
        </button>
      </div>
    </div>

    <!-- Salon Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mb-20">
      <NuxtLink
        v-for="salon in salons"
        :key="salon.id"
        :to="`/salon/${salon.id}`"
        class="bg-white rounded-xl overflow-hidden shadow-md hover:shadow-lg transition-shadow cursor-pointer transform hover:scale-[1.02] transition-transform duration-200"
      >
        <div class="relative h-64">
          <img
            :src="salon.image"
            :alt="salon.name"
            class="w-full h-[248px] object-cover object-center"
          />
          <div
            class="absolute top-0 right-0 bg-black-900/70 text-white px-3 py-2 flex flex-col items-center gap-1"
          >
            <span class="text-lg font-semibold">{{ salon.averageReview }}</span>
            <span class="text-sm">{{ salon.totalReviews }} Reviews</span>
          </div>
        </div>
        <div class="p-4">
          <h3 class="text-xl font-semibold">{{ salon.name }}</h3>
          <p class="text-gray-600">{{ salon.address }}</p>
        </div>
      </NuxtLink>
    </div>
  </div>

  <Footer />
</template>

<script setup lang="ts">
import { ref } from "vue";

const salons = ref([
  {
    id: 1,
    image: "/images/img1.webp",
    name: "Felicia Salon",
    address: "Barnawa no.25 Yakubu street",
    totalReviews: 120,
    averageReview: 4.5,
  },
  {
    id: 2,
    image: "/images/img2.webp",
    name: "Glamour Hub",
    address: "456 Style Avenue",
    totalReviews: 98,
    averageReview: 4.7,
  },
  {
    id: 3,
    image: "/images/img3.webp",
    name: "Elegance Studio",
    address: "789 Fashion Blvd",
    totalReviews: 75,
    averageReview: 4.3,
  },
  {
    id: 4,
    image: "/images/img4.webp",
    name: "Beauty Bliss",
    address: "101 Glamour Road",
    totalReviews: 150,
    averageReview: 4.8,
  },
  {
    id: 5,
    image: "/images/img2.webp",
    name: "Glamour Hub",
    address: "456 Style Avenue",
    totalReviews: 98,
    averageReview: 4.7,
  },
  {
    id: 6,
    image: "/images/img3.webp",
    name: "Radiant Beauty",
    address: "202 Glow Street",
    totalReviews: 85,
    averageReview: 4.6,
  },
  {
    id: 7,
    image: "/images/img1.webp",
    name: "Chic Salon",
    address: "303 Style Lane",
    totalReviews: 110,
    averageReview: 4.4,
  },
  {
    id: 8,
    image: "/images/img4.webp",
    name: "Glam Central",
    address: "404 Fashion Avenue",
    totalReviews: 95,
    averageReview: 4.5,
  },
  {
    id: 9,
    image: "/images/img2.webp",
    name: "Elegance Parlor",
    address: "505 Beauty Blvd",
    totalReviews: 130,
    averageReview: 4.7,
  },
]);
</script>

<style scoped></style>
