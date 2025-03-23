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

    <div class="mb-6">
      <h1 class="text-2xl font-bold">Appointment Request</h1>
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
        <p class="text-gray-500">No appointment requests at the moment.</p>
      </div>

      <!-- Appointment list -->
      <div
        v-else
        v-for="appointment in appointments"
        :key="appointment.id"
        class="bg-white p-4 rounded-md shadow-sm border border-gray-100"
      >
        <div
          class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-3"
        >
          <div class="flex items-center gap-3">
            <div
              class="w-8 h-8 bg-gray-200 rounded-full flex items-center justify-center"
            >
              <svg
                xmlns="http://www.w3.org/2000/svg"
                class="h-5 w-5 text-gray-500"
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
            <span class="font-medium">{{ appointment.clientName }}</span>
          </div>

          <div class="flex flex-wrap gap-3">
            <div class="flex items-center gap-1 text-sm text-gray-600">
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
                <rect x="3" y="4" width="18" height="18" rx="2" ry="2"></rect>
                <line x1="16" y1="2" x2="16" y2="6"></line>
                <line x1="8" y1="2" x2="8" y2="6"></line>
                <line x1="3" y1="10" x2="21" y2="10"></line>
              </svg>
              {{ appointment.date }}
            </div>

            <div class="flex items-center gap-1 text-sm text-gray-600">
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
                <circle cx="12" cy="12" r="10"></circle>
                <polyline points="12 6 12 12 16 14"></polyline>
              </svg>
              {{ appointment.time }}
            </div>
          </div>
        </div>

        <div class="mb-4">
          <span
            :class="`inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium ${
              appointment.serviceType === 'Home service'
                ? 'bg-amber-100 text-amber-800'
                : 'bg-green-100 text-green-800'
            }`"
          >
            <svg
              v-if="appointment.serviceType === 'Home service'"
              xmlns="http://www.w3.org/2000/svg"
              class="h-3 w-3 mr-1"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
              <polyline points="9 22 9 12 15 12 15 22"></polyline>
            </svg>
            <svg
              v-else
              xmlns="http://www.w3.org/2000/svg"
              class="h-3 w-3 mr-1"
              viewBox="0 0 24 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            >
              <rect x="2" y="7" width="20" height="14" rx="2" ry="2"></rect>
              <path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"></path>
            </svg>
            {{ appointment.serviceType }}
          </span>
        </div>

        <div class="flex justify-end gap-2">
          <button
            @click="rejectAppointment(appointment.id)"
            class="inline-flex items-center px-3 py-1.5 border border-red-300 text-sm font-medium rounded-md text-red-700 bg-white hover:bg-red-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-red-500"
            :disabled="processing"
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
              <circle cx="12" cy="12" r="10"></circle>
              <line x1="15" y1="9" x2="9" y2="15"></line>
              <line x1="9" y1="9" x2="15" y2="15"></line>
            </svg>
            Reject
          </button>
          <button
            @click="acceptAppointment(appointment.id)"
            class="inline-flex items-center px-3 py-1.5 border border-transparent text-sm font-medium rounded-md text-white bg-green-600 hover:bg-green-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-green-500"
            :disabled="processing"
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
              <polyline points="20 6 9 17 4 12"></polyline>
            </svg>
            Accept
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

// State
const appointments = ref([]);
const loading = ref(true);
const error = ref(null);
const processing = ref(false);

// Mock data - replace with API call
onMounted(async () => {
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 500));

    // Mock data
    appointments.value = [
      {
        id: 1,
        clientName: "Miss Victoria",
        date: "Wed 18, 2024",
        time: "10:00 am",
        serviceType: "Home service",
      },
      {
        id: 2,
        clientName: "Miss Victoria",
        date: "Wed 18, 2024",
        time: "10:00 am",
        serviceType: "Salon Service",
      },
      {
        id: 3,
        clientName: "Miss Sarah",
        date: "Thu 19, 2024",
        time: "2:30 pm",
        serviceType: "Home service",
      },
    ];

    loading.value = false;
  } catch (err) {
    error.value = "Failed to load appointment requests. Please try again.";
    loading.value = false;
  }
});

// Methods
const acceptAppointment = async (id) => {
  processing.value = true;
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 500));

    // Remove from list (in real app, you'd update status via API)
    appointments.value = appointments.value.filter(
      (appointment) => appointment.id !== id,
    );

    // Show success notification (implement your notification system)
    console.log("Appointment accepted successfully");
  } catch (err) {
    error.value = "Failed to accept appointment. Please try again.";
  } finally {
    processing.value = false;
  }
};

const rejectAppointment = async (id) => {
  processing.value = true;
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 500));

    // Remove from list (in real app, you'd update status via API)
    appointments.value = appointments.value.filter(
      (appointment) => appointment.id !== id,
    );

    // Show success notification (implement your notification system)
    console.log("Appointment rejected successfully");
  } catch (err) {
    error.value = "Failed to reject appointment. Please try again.";
  } finally {
    processing.value = false;
  }
};
</script>
