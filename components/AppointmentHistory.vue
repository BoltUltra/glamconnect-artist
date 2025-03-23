<template>
  <div class="p-4 md:p-6 max-w-6xl">
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
      <h1 class="text-2xl font-bold">Appointment History</h1>

      <div class="flex items-center gap-2">
        <div class="relative">
          <select
            v-model="timeFilter"
            class="appearance-none block w-full bg-white border border-gray-300 rounded-md py-2 pl-3 pr-10 text-sm focus:outline-none focus:ring-2 focus:ring-amber-500 focus:border-amber-500"
          >
            <option value="last-month">Last Month</option>
            <option value="last-3-months">Last 3 Months</option>
            <option value="last-6-months">Last 6 Months</option>
            <option value="last-year">Last Year</option>
            <option value="all-time">All Time</option>
          </select>
          <div
            class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
          >
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
              <polyline points="6 9 12 15 18 9"></polyline>
            </svg>
          </div>
        </div>

        <button
          class="p-2 bg-white border border-gray-300 rounded-md text-gray-700 hover:bg-gray-50"
        >
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <rect x="3" y="4" width="18" height="18" rx="2" ry="2"></rect>
            <line x1="16" y1="2" x2="16" y2="6"></line>
            <line x1="8" y1="2" x2="8" y2="6"></line>
            <line x1="3" y1="10" x2="21" y2="10"></line>
          </svg>
        </button>
      </div>
    </div>

    <div class="space-y-4">
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
        v-else-if="appointments.length === 0"
        class="bg-gray-50 p-6 rounded-md text-center"
      >
        <p class="text-gray-500">
          No appointment history found for the selected period.
        </p>
      </div>

      <!-- Appointment history list -->
      <div
        v-else
        v-for="appointment in appointments"
        :key="appointment.id"
        class="bg-white p-4 rounded-md shadow-sm border border-gray-100"
      >
        <div class="flex items-start gap-3">
          <div
            class="w-8 h-8 bg-amber-100 rounded-full flex items-center justify-center flex-shrink-0"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              class="h-5 w-5 text-amber-600"
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

          <div class="flex-1">
            <div
              class="flex flex-col sm:flex-row sm:items-center sm:justify-between gap-2"
            >
              <h3 class="font-medium text-gray-900">
                {{
                  appointment.status === "rejected"
                    ? "Rejected an appointment with "
                    : "Appointment with "
                }}
                {{ appointment.clientName }}
              </h3>

              <div v-if="appointment.status === 'completed'" class="flex">
                <template v-for="i in 5" :key="i">
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    :class="`h-5 w-5 ${i <= appointment.rating ? 'text-amber-400' : 'text-gray-300'}`"
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

            <div
              v-if="appointment.status === 'rejected'"
              class="text-sm text-gray-500 mt-1"
            >
              (Reschedule the appointment for {{ appointment.rescheduleDate }})
            </div>

            <div
              v-if="appointment.status === 'completed' && appointment.feedback"
              class="text-sm text-gray-600 mt-2 italic"
            >
              "{{ appointment.feedback }}"
            </div>

            <div v-if="appointment.status === 'rejected'" class="mt-3">
              <button
                class="text-sm text-amber-600 hover:text-amber-700 font-medium"
              >
                Reschedule Now
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, watch } from "vue";

// State
const appointments = ref([]);
const loading = ref(true);
const error = ref(null);
const timeFilter = ref("last-month");

// Methods
const fetchAppointmentHistory = async () => {
  loading.value = true;
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 500));

    // Mock data
    appointments.value = [
      {
        id: 1,
        clientName: "Miss Victoria",
        status: "rejected",
        rescheduleDate: "25th Sept",
        date: "15th Sept, 2024",
      },
      {
        id: 2,
        clientName: "Miss Victoria",
        status: "completed",
        rating: 3,
        feedback: "I love the make up thank you!",
        date: "10th Sept, 2024",
      },
      {
        id: 3,
        clientName: "Miss Victoria",
        status: "rejected",
        rescheduleDate: "25th Sept",
        date: "5th Sept, 2024",
      },
      {
        id: 4,
        clientName: "Miss Victoria",
        status: "completed",
        rating: 3,
        feedback: "I love the make up thank you!",
        date: "1st Sept, 2024",
      },
    ];

    loading.value = false;
  } catch (err) {
    error.value = "Failed to load appointment history. Please try again.";
    loading.value = false;
  }
};

// Watch for filter changes
watch(timeFilter, () => {
  fetchAppointmentHistory();
});

// Lifecycle hooks
onMounted(() => {
  fetchAppointmentHistory();
});
</script>
