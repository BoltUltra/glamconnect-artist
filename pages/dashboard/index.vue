<template>
  <div class="space-y-6">
    <header class="flex justify-between items-center">
      <div>
        <h1 class="text-2xl font-bold">Trailblazing</h1>
        <p class="text-gray-600">Welcome back to GlamConnect</p>
      </div>
      <button class="p-2 rounded-full hover:bg-gray-100">
        <Bell class="w-6 h-6" />
      </button>
    </header>

    <div class="grid md:grid-cols-3 gap-6">
      <div
        class="md:col-span-2 bg-white rounded-lg shadow p-6 overflow-x-scroll"
      >
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-xl font-semibold">Today's Schedule</h2>
          <div class="flex items-center space-x-4">
            <div
              class="flex items-center space-x-2 border rounded-md px-3 py-1"
            >
              <span>Sept 5th</span>
              <Calendar class="w-4 h-4" />
            </div>
            <button
              class="bg-white border rounded-md px-3 py-1 hover:bg-gray-50"
            >
              View all
            </button>
          </div>
        </div>

        <!-- Schedule Timeline -->
        <div class="overflow-x-auto">
          <div class="flex space-x-4 mb-2 min-w-max">
            <div
              v-for="hour in timeSlots"
              :key="hour"
              class="w-24 text-center text-sm text-gray-600"
            >
              {{ hour }}
            </div>
          </div>

          <div class="relative h-32 min-w-max">
            <!-- Example events -->
            <div
              class="absolute top-0 left-0 w-96 h-full bg-green-100 rounded p-2"
              style="left: 0%; width: 33.33%"
            >
              <h4 class="text-sm font-semibold">Bridal make up</h4>
              <p class="text-xs text-gray-600">9am-12pm</p>
            </div>
            <div
              class="absolute top-0 left-0 w-48 h-full bg-yellow-100 rounded p-2"
              style="left: 50%; width: 16.66%"
            >
              <h4 class="text-sm font-semibold">Casual make up</h4>
              <p class="text-xs text-gray-600">1pm-2pm</p>
            </div>
            <div
              class="absolute top-0 left-0 w-48 h-full bg-yellow-100 rounded p-2"
              style="left: 75%; width: 16.66%"
            >
              <h4 class="text-sm font-semibold">Casual make up</h4>
              <p class="text-xs text-gray-600">3pm-4pm</p>
            </div>
          </div>
        </div>
      </div>

      <div class="bg-white rounded-lg shadow p-6">
        <div class="flex justify-between items-center mb-4">
          <h2 class="text-xl font-semibold">Messages</h2>
          <div class="flex space-x-2">
            <button class="p-1 hover:bg-gray-100 rounded-full">
              <Search class="w-5 h-5" />
            </button>
            <button class="p-1 hover:bg-gray-100 rounded-full">
              <MoreVertical class="w-5 h-5" />
            </button>
          </div>
        </div>

        <!-- Messages List -->
        <div class="space-y-4">
          <div
            v-for="i in 5"
            :key="i"
            class="flex items-start space-x-3 pb-3 border-b last:border-b-0"
          >
            <div
              class="w-10 h-10 bg-gray-200 rounded-full flex items-center justify-center"
            >
              <User2 class="w-6 h-6 text-gray-600" />
            </div>
            <div class="flex-1 min-w-0">
              <div class="flex justify-between items-center mb-1">
                <h4 class="text-sm font-semibold">Miss Victoria</h4>
                <span class="text-xs text-gray-500">5th March, 2024</span>
              </div>
              <p class="text-sm text-gray-600 truncate">
                I had the most amazing experience. The atmosphere was so...
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import { Bell, Calendar, Search, MoreVertical, User2 } from "lucide-vue-next";

definePageMeta({
  layout: "dashboard",
});
const timeSlots = ref([
  "9 AM",
  "10 AM",
  "11 AM",
  "12 AM",
  "1 PM",
  "2 PM",
  "3 PM",
  "4 PM",
  "5 PM",
]);
</script>
