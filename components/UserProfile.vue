<template>
  <div class="p-4 md:p-6 w-full max-w-6xl">
    <div class="mb-6">
      <h1 class="text-2xl font-bold">User Profile</h1>
      <p class="text-gray-600 text-sm">
        Manage your preference and configure various options
      </p>
    </div>

    <!-- Loading state -->
    <div v-if="loading" class="flex justify-center items-center py-10">
      <div
        class="animate-spin rounded-full h-10 w-10 border-b-2 border-gray-900"
      ></div>
    </div>

    <!-- Error state -->
    <div v-else-if="error" class="bg-red-50 p-4 rounded-md text-red-600">
      {{ error }}
    </div>

    <!-- Profile content -->
    <div v-else class="space-y-8 mt-20">
      <!-- Profile header -->
      <div class="flex flex-col gap-6">
        <div
          class="w-20 h-20 bg-gray-200 rounded-full flex items-center justify-center"
        >
          <svg
            v-if="!profile.avatar"
            xmlns="http://www.w3.org/2000/svg"
            class="h-10 w-10 text-gray-500"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
            <circle cx="12" cy="7" r="4"></circle>
          </svg>
          <img
            v-else
            :src="profile.avatar"
            alt="Profile avatar"
            class="w-full h-full object-cover rounded-full"
          />
        </div>

        <div class="flex-1">
          <div
            class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4"
          >
            <h2 class="text-xl font-bold">{{ profile.name }}</h2>

            <button
              class="flex w-32 items-center px-3 py-2 md:my-0 my-5 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-amber-500"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-4 w-4 mr-1.5"
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path
                  d="M11 4H4a2 2 0 0 0-2 2v14a2 2 0 0 0 2 2h14a2 2 0 0 0 2-2v-7"
                ></path>
                <path
                  d="M18.5 2.5a2.121 2.121 0 0 1 3 3L12 15l-4 1 1-4 9.5-9.5z"
                ></path>
              </svg>
              Edit Profile
            </button>
          </div>

          <div class="flex items-center gap-1 text-sm text-gray-600 mt-1">
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-4 w-4"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"></path>
              <circle cx="12" cy="10" r="3"></circle>
            </svg>
            {{ profile.location }}
          </div>

          <p class="text-gray-700 mt-3">{{ profile.bio }}</p>
          <div
            class="flex md:flex-row flex-col md:justify-between md:gap-0 gap-5"
          >
            <div class="flex flex-wrap gap-3 mt-4">
              <a
                v-for="social in profile.socialLinks"
                :key="social.name"
                :href="social.url"
                target="_blank"
                rel="noopener noreferrer"
                class="inline-flex items-center text-sm text-amber-600 hover:text-amber-700"
              >
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  class="h-4 w-4 mr-1"
                  viewBox="0 0 24 24"
                  fill="none"
                  stroke="currentColor"
                  stroke-width="2"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                >
                  <path
                    d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"
                  ></path>
                </svg>
                {{ social.name }}
              </a>
            </div>

            <div class="mt-4 flex items-center gap-2">
              <span class="text-sm text-gray-600">Ratings</span>
              <div class="flex">
                <template v-for="i in 5" :key="i">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    :class="`h-5 w-5 ${i <= profile.rating ? 'text-amber-400' : 'text-gray-300'}`"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                    />
                  </svg>
                </template>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Portfolio section -->
      <div>
        <div class="flex items-center justify-between mb-4">
          <h3 class="text-lg font-bold">Portfolio</h3>
          <button
            class="inline-flex items-center px-3 py-1.5 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-amber-600 hover:bg-amber-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-amber-500"
          >
            Add
          </button>
        </div>

        <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 gap-4">
          <div
            v-for="(image, index) in portfolio"
            :key="index"
            class="aspect-square rounded-md overflow-hidden bg-gray-100"
          >
            <img
              :src="image"
              alt="Portfolio image"
              class="w-full h-full object-cover"
            />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

// State
const profile = ref({});
const portfolio = ref([]);
const services = ref([]);
const availability = ref([]);
const loading = ref(true);
const error = ref(null);

// Methods
const fetchProfileData = async () => {
  loading.value = true;
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 500));

    // Mock profile data
    profile.value = {
      name: "Trailblazing",
      location: "Lagos, Nigeria",
      bio: "Hi, I'm Trailblazing, a professional makeup artist with over 2 years of experience specializing in bridal, editorial, and event makeup. My passion is enhancing natural beauty while creating unique, personalized looks for each client. Whether you're looking for soft glam or bold, creative artistry, I'm here to make sure you feel confident and radiant on your special day",
      rating: 3,
      socialLinks: [
        { name: "Trailblazing.facebook", url: "#" },
        { name: "Trailblazing.insta", url: "#" },
      ],
    };

    // Mock portfolio images
    portfolio.value = [
      "/images/img1.webp",
      "/images/img2.webp",
      "/images/img3.webp",
      "/images/img4.webp",
      "/images/img1.webp",
      "/images/img2.webp",
      "/images/img3.webp",
      "/images/img4.webp",
      "/images/img1.webp",
      "/images/img2.webp",
      "/images/img3.webp",
      "/images/img4.webp",
      "/images/img1.webp",
      "/images/img2.webp",
      "/images/img3.webp",
      "/images/img4.webp",
    ];

    // Mock services
    services.value = [
      {
        id: 1,
        name: "Bridal Makeup",
        description:
          "Full bridal makeup with premium products and lashes included",
        price: 150,
        duration: "90 min",
      },
      {
        id: 2,
        name: "Special Event Makeup",
        description: "Full face makeup for special occasions",
        price: 80,
        duration: "60 min",
      },
      {
        id: 3,
        name: "Natural Everyday Look",
        description: "Light, natural-looking makeup for everyday wear",
        price: 50,
        duration: "45 min",
      },
    ];

    // Mock availability
    availability.value = [
      { name: "Monday", available: true, hours: "9:00 AM - 5:00 PM" },
      { name: "Tuesday", available: true, hours: "9:00 AM - 5:00 PM" },
      { name: "Wednesday", available: true, hours: "9:00 AM - 5:00 PM" },
      { name: "Thursday", available: true, hours: "9:00 AM - 5:00 PM" },
      { name: "Friday", available: true, hours: "9:00 AM - 5:00 PM" },
      { name: "Saturday", available: true, hours: "10:00 AM - 3:00 PM" },
      { name: "Sunday", available: false, hours: null },
    ];

    loading.value = false;
  } catch (err) {
    error.value = "Failed to load profile data. Please try again.";
    loading.value = false;
  }
};

// Lifecycle hooks
onMounted(() => {
  fetchProfileData();
});
</script>
