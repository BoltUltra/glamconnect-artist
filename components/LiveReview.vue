<template>
  <div class="p-4 md:p-6 w-full max-w-6xl">
    <div class="flex items-center gap-5 mb-20">
      <div>
        <svg
          width="40"
          height="40"
          viewBox="0 0 32 33"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <rect y="0.5" width="32" height="32" rx="16" fill="#D4DAE7" />
          <path
            d="M21.3333 23.1666H10.6667C10.2985 23.1666 10 22.8681 10 22.4999V10.4999C10 10.1317 10.2985 9.83325 10.6667 9.83325H21.3333C21.7015 9.83325 22 10.1317 22 10.4999V22.4999C22 22.8681 21.7015 23.1666 21.3333 23.1666ZM13.3333 13.1666V14.4999H18.6667V13.1666H13.3333ZM13.3333 15.8333V17.1666H18.6667V15.8333H13.3333ZM13.3333 18.4999V19.8333H18.6667V18.4999H13.3333Z"
            fill="#5D6474"
          />
        </svg>
      </div>
      <div class="">
        <h1 class="text-2xl font-bold">Booking Management</h1>
        <p class="text-gray-600 text-sm">
          Manage your preference and configure various options
        </p>
      </div>
    </div>

    <div
      class="mb-6 flex flex-col sm:flex-row sm:items-center sm:justify-between gap-4"
    >
      <h1 class="text-2xl font-bold">Live Review</h1>

      <button
        class="inline-flex items-center px-4 py-2 border border-gray-300 rounded-md shadow-sm text-sm font-medium text-gray-700 bg-white hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-amber-500"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-4 w-4 mr-2"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
          <polygon
            points="22 3 2 3 10 12.46 10 19 14 21 14 12.46 22 3"
          ></polygon>
        </svg>
        Filter
      </button>
    </div>

    <div class="space-y-6">
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

      <!-- Empty state -->
      <div
        v-else-if="reviews.length === 0"
        class="bg-gray-50 p-6 rounded-md text-center"
      >
        <p class="text-gray-500">
          No reviews yet. Your reviews will appear here once clients leave
          feedback.
        </p>
      </div>

      <!-- Reviews list -->
      <div
        v-else
        v-for="review in reviews"
        :key="review.id"
        class="bg-white p-4 md:p-6 rounded-md shadow-sm border border-gray-100"
      >
        <div class="flex flex-col md:flex-row md:items-start gap-4">
          <div class="flex-shrink-0">
            <div
              class="w-10 h-10 bg-gray-200 rounded-full flex items-center justify-center"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-6 w-6 text-gray-500"
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
            </div>
          </div>

          <div class="flex-1">
            <div class="flex flex-col sm:flex-row sm:items-center gap-2 mb-2">
              <h3 class="font-medium text-gray-900">{{ review.clientName }}</h3>
              <span class="text-sm text-gray-500">{{ review.date }}</span>
            </div>

            <div class="flex mb-3">
              <template v-for="i in 5" :key="i">
                <svg
                  xmlns="http://www.w3.org/2000/svg"
                  :class="`h-5 w-5 ${i <= review.rating ? 'text-amber-400' : 'text-gray-300'}`"
                  viewBox="0 0 20 20"
                  fill="currentColor"
                >
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  />
                </svg>
              </template>
            </div>

            <p class="text-gray-700">{{ review.comment }}</p>

            <div class="mt-4 flex flex-wrap gap-2">
              <span
                v-for="(tag, index) in review.tags"
                :key="index"
                class="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-gray-100 text-gray-800"
              >
                {{ tag }}
              </span>
            </div>

            <div
              v-if="review.images && review.images.length > 0"
              class="mt-4 flex flex-wrap gap-2"
            >
              <div
                v-for="(image, index) in review.images"
                :key="index"
                class="w-16 h-16 rounded-md overflow-hidden"
              >
                <img
                  :src="image"
                  alt="Review image"
                  class="w-full h-full object-cover"
                />
              </div>
            </div>

            <div
              v-if="review.reply"
              class="mt-4 pl-4 border-l-2 border-gray-200"
            >
              <p class="text-sm text-gray-600 italic">{{ review.reply }}</p>
              <p class="text-xs text-gray-500 mt-1">
                Your reply - {{ review.replyDate }}
              </p>
            </div>

            <div v-else class="mt-4">
              <button
                class="text-sm text-amber-600 hover:text-amber-700 font-medium"
              >
                Reply to this review
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

// State
const reviews = ref([]);
const loading = ref(true);
const error = ref(null);

// Methods
const fetchReviews = async () => {
  loading.value = true;
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 500));

    // Mock data
    reviews.value = [
      {
        id: 1,
        clientName: "Miss Victoria",
        date: "5th March, 2024",
        rating: 3,
        comment:
          "I had the most amazing experience. The atmosphere was so warm and welcoming, and the team truly went above and beyond to make me feel special. My makeup turned out even better than I imagined – flawless, long-lasting...",
        tags: ["Makeup", "Professional", "Friendly"],
        images: ["/images/img1.webp", "/images/img1.webp"],
        reply: null,
        replyDate: null,
      },
      {
        id: 2,
        clientName: "Miss Victoria",
        date: "5th March, 2024",
        rating: 3,
        comment:
          "I had the most amazing experience. The atmosphere was so warm and welcoming, and the team truly went above and beyond to make me feel special. My makeup turned out even better than I imagined – flawless, long-lasting...",
        tags: ["Makeup", "Professional", "Friendly"],
        images: [],
        reply:
          "Thank you so much for your kind words! We're thrilled that you enjoyed your experience with us and loved your makeup. We can't wait to see you again soon!",
        replyDate: "6th March, 2024",
      },
    ];

    loading.value = false;
  } catch (err) {
    error.value = "Failed to load reviews. Please try again.";
    loading.value = false;
  }
};

// Lifecycle hooks
onMounted(() => {
  fetchReviews();
});
</script>
