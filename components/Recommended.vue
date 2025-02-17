<script setup lang="ts">
import { ref } from "vue";

const recommendedSalons = ref([
  {
    id: Math.round(Math.random() * 100),
    image: "/images/img1.webp",
    name: "Felicia Salon",
    address: "Barnawa no.25 Yakubu street",
    totalReviews: 120,
    averageReview: 4.5,
  },
  {
    id: Math.round(Math.random() * 100),
    image: "/images/img2.webp",
    name: "Glamour Hub",
    address: "456 Style Avenue",
    totalReviews: 98,
    averageReview: 4.7,
  },
  {
    id: Math.round(Math.random() * 100),
    image: "/images/img3.webp",
    name: "Elegance Studio",
    address: "789 Fashion Blvd",
    totalReviews: 75,
    averageReview: 4.3,
  },
  {
    id: Math.round(Math.random() * 100),
    image: "/images/img4.webp",
    name: "Beauty Bliss",
    address: "101 Glamour Road",
    totalReviews: 150,
    averageReview: 4.8,
  },
  {
    id: Math.round(Math.random() * 100),
    image: "/images/img2.webp",
    name: "Glamour Hub",
    address: "456 Style Avenue",
    totalReviews: 98,
    averageReview: 4.7,
  },
]);
</script>
<template>
  <section class="md:pl-20 pl-5 my-10 mt-20">
    <h2 class="text-3xl font-semibold text-gray-900">Recommended</h2>
    <div class="mt-6 flex overflow-x-auto gap-6">
      <NuxtLink
        v-for="salon in recommendedSalons"
        :key="salon.name"
        :to="`/salon/${salon.id}`"
        class="bg-white shadow-md rounded-lg overflow-hidden animate-zoom-in min-w-[400px] mb-5"
      >
        <div class="relative">
          <img
            :src="salon.image"
            alt="salon"
            class="rounded-md mb-4 h-[248px] w-full object-center object-cover"
          />
          <div
            class="h-20 w-32 bg-black-900/70 absolute top-0 right-0 text-white text-center p-2"
          >
            <p class="font-bold text-3xl">{{ salon.averageReview }}</p>
            <p class="text-sm">{{ salon.totalReviews }} Reviews</p>
          </div>
        </div>
        <div class="p-3">
          <h3 class="text-xl font-medium">{{ salon.name }}</h3>
          <p class="text-gray-600">{{ salon.address }}</p>
          <p class="text-gray-600">Total Reviews: {{ salon.totalReviews }}</p>
          <p class="text-gray-600">Average Review:</p>
        </div>
      </NuxtLink>
    </div>
  </section>
</template>
<style scoped></style>
