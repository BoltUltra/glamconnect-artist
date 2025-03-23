<template>
  <div
    class="container__custom py-8 min-h-screen flex flex-col dark:text-white"
  >
    <!-- Header -->
    <header class="mb-8">
      <h1 class="text-3xl md:text-4xl font-bold">GlamConnect</h1>
    </header>

    <!-- Back button -->
    <div class="mb-8">
      <button
        @click="goBack"
        class="flex items-center text-gray-700 hover:text-gray-900 dark:hover:text-gray-500 transition-colors dark:text-white"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mr-1"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M10 19l-7-7m0 0l7-7m-7 7h18"
          />
        </svg>
        Back
      </button>
    </div>

    <!-- Main content -->
    <div class="flex-grow flex flex-col max-w-xl mx-auto">
      <!-- Title section -->
      <div v-motion="titleAnimation" class="text-left mb-10">
        <h2 class="text-2xl md:text-3xl font-semibold mb-2">
          Select User Type
        </h2>
        <p class="text-gray-600 dark:text-white">
          You can change your account at any time
        </p>
      </div>

      <!-- User type selection cards -->
      <div class="grid grid-cols-1 md:grid-cols-2 gap-6 w-full max-w-xl">
        <!-- Customer card -->
        <div
          v-motion="customerAnimation"
          class="border rounded-lg px-8 py-12 flex flex-col items-center cursor-pointer hover:shadow-md transition-shadow"
          :class="{
            'border-orange-500 border-b-8 border-b-primary-500':
              selectedType === 'customer',
          }"
          @click="selectType('customer')"
        >
          <img src="/images/customer.svg" alt="" />
          <h3 class="text-xl font-medium mb-2">Customer</h3>
          <p class="text-gray-600 dark:text-white text-center text-sm">
            Get Connected with makeup Artist around you from the anywhere around
            the world
          </p>
        </div>

        <!-- Make-up Artist card -->
        <div
          v-motion="artistAnimation"
          class="border rounded-lg p-6 flex flex-col items-center cursor-pointer hover:shadow-md transition-shadow"
          :class="{
            'border-orange-500 border-b-8 border-b-primary-500':
              selectedType === 'artist',
          }"
          @click="selectType('artist')"
        >
          <img src="/images/artist.svg" alt="" />
          <h3 class="text-xl font-medium mb-2">Make-up Artist</h3>
          <p class="text-gray-600 dark:text-white text-center text-sm">
            Get connected with clients around the world
          </p>
        </div>
      </div>

      <!-- Next button -->
      <button
        v-motion="buttonAnimation"
        class="bg-orange-500 text-white rounded-md py-3 px-6 w-full max-w-3xl mt-10 hover:bg-orange-600 transition-colors"
        :disabled="!selectedType"
        :class="{ 'opacity-75 cursor-not-allowed': !selectedType }"
        @click="
          router.push(
            selectedType === 'customer'
              ? 'https://glamconnect-customer.vercel.app/auth/login'
              : '/auth/register',
          )
        "
      >
        Next
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const router = useRouter();

const goBack = () => {
  router.push("/");
};

const selectedType = ref("artist");

const titleAnimation = {
  initial: { opacity: 0, y: -20 },
  visible: { opacity: 1, y: 0, transition: { duration: 500, delay: 100 } },
};

const customerAnimation = {
  initial: { opacity: 0, x: -50 },
  visible: { opacity: 1, x: 0, transition: { duration: 400, delay: 200 } },
};

const artistAnimation = {
  initial: { opacity: 0, x: 50 },
  visible: { opacity: 1, x: 0, transition: { duration: 400, delay: 300 } },
};

const buttonAnimation = {
  initial: { opacity: 0, y: 50 },
  visible: { opacity: 1, y: 0, transition: { duration: 400, delay: 400 } },
};

const selectType = (type) => {
  selectedType.value = type;
};
</script>
