<template>
  <div class="p-4 md:p-6 w-full">
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

    <div class="grid grid-cols-1 lg:grid-cols-3 gap-6">
      <!-- Calendar Section -->
      <div class="lg:col-span-2">
        <div
          class="bg-white rounded-md shadow-sm border border-gray-100 overflow-hidden"
        >
          <!-- Calendar Header -->
          <div
            class="flex items-center justify-between p-4 border-b border-gray-100"
          >
            <button class="p-1 rounded-md hover:bg-gray-100">
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
                <polyline points="15 18 9 12 15 6"></polyline>
              </svg>
            </button>
            <h2 class="text-lg font-medium">{{ currentMonth }}</h2>
            <button class="p-1 rounded-md hover:bg-gray-100">
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
                <polyline points="9 18 15 12 9 6"></polyline>
              </svg>
            </button>
          </div>

          <!-- Calendar Days -->
          <div
            class="grid grid-cols-7 text-center py-2 border-b border-gray-100"
          >
            <div v-for="day in weekDays" :key="day" class="text-sm font-medium">
              {{ day }}
            </div>
          </div>

          <!-- Calendar Dates -->
          <div class="grid grid-cols-7 text-center">
            <div
              v-for="(date, index) in calendarDates"
              :key="index"
              :class="`p-2 relative ${date.isCurrentMonth ? '' : 'text-gray-400'} ${date.isToday ? 'bg-amber-50' : ''} ${date.hasAppointments ? 'font-medium' : ''}`"
            >
              <div
                :class="`h-8 w-8 flex items-center justify-center mx-auto rounded-full ${date.isSelected ? 'bg-amber-100' : 'hover:bg-gray-100'}`"
              >
                {{ date.day }}
              </div>
              <div
                v-if="date.appointmentCount > 0"
                class="absolute bottom-1 left-1/2 transform -translate-x-1/2 text-xs text-gray-500"
              >
                +{{ date.appointmentCount }}
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Appointments List -->
      <div class="lg:col-span-1">
        <div class="bg-white rounded-md shadow-sm border border-gray-100 p-4">
          <h3 class="text-lg font-medium mb-4">Upcoming Appointments</h3>

          <div v-if="loading" class="flex justify-center items-center py-10">
            <div
              class="animate-spin rounded-full h-8 w-8 border-b-2 border-gray-900"
            ></div>
          </div>

          <div
            v-else-if="upcomingAppointments.length === 0"
            class="text-center py-8 text-gray-500"
          >
            No appointments for selected date
          </div>

          <div v-else class="space-y-4">
            <div
              v-for="appointment in upcomingAppointments"
              :key="appointment.id"
              class="border-b border-gray-100 pb-4 last:border-0"
            >
              <div class="flex items-start gap-3 mb-2">
                <div
                  class="w-8 h-8 bg-gray-200 rounded-full flex items-center justify-center mt-1"
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
                <div>
                  <p class="font-medium">{{ appointment.clientName }}</p>
                  <div class="flex flex-wrap gap-3 mt-1">
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
                        <rect
                          x="3"
                          y="4"
                          width="18"
                          height="18"
                          rx="2"
                          ry="2"
                        ></rect>
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
                  <div class="mt-2">
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
                        <path
                          d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"
                        ></path>
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
                        <rect
                          x="2"
                          y="7"
                          width="20"
                          height="14"
                          rx="2"
                          ry="2"
                        ></rect>
                        <path
                          d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"
                        ></path>
                      </svg>
                      {{ appointment.serviceType }}
                    </span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";

// State
const loading = ref(true);
const currentDate = ref(new Date());
const selectedDate = ref(null);
const upcomingAppointments = ref([]);

// Computed properties
const currentMonth = computed(() => {
  return new Intl.DateTimeFormat("en-US", { month: "long" }).format(
    currentDate.value,
  );
});

const weekDays = computed(() => ["Su", "Mo", "Tu", "We", "Th", "Fr", "Sa"]);

const calendarDates = computed(() => {
  const year = currentDate.value.getFullYear();
  const month = currentDate.value.getMonth();

  // First day of the month
  const firstDay = new Date(year, month, 1);
  // Last day of the month
  const lastDay = new Date(year, month + 1, 0);

  // Get the day of the week for the first day (0-6, where 0 is Sunday)
  const firstDayOfWeek = firstDay.getDay();

  // Calculate days from previous month to show
  const daysFromPrevMonth = firstDayOfWeek;

  // Calculate total days to show (previous month days + current month days)
  const totalDays = daysFromPrevMonth + lastDay.getDate();

  // Calculate rows needed (7 days per row)
  const rows = Math.ceil(totalDays / 7);

  // Calculate total cells needed
  const totalCells = rows * 7;

  // Generate calendar dates
  const dates = [];

  // Previous month days
  const prevMonth = new Date(year, month, 0);
  const prevMonthDays = prevMonth.getDate();

  for (let i = 0; i < daysFromPrevMonth; i++) {
    const day = prevMonthDays - daysFromPrevMonth + i + 1;
    dates.push({
      day,
      isCurrentMonth: false,
      isToday: false,
      isSelected: false,
      hasAppointments: false,
      appointmentCount: 0,
    });
  }

  // Current month days
  const today = new Date();
  const isCurrentMonthAndYear =
    today.getMonth() === month && today.getFullYear() === year;

  for (let i = 1; i <= lastDay.getDate(); i++) {
    const isToday = isCurrentMonthAndYear && today.getDate() === i;
    const isSelected =
      selectedDate.value &&
      selectedDate.value.getDate() === i &&
      selectedDate.value.getMonth() === month &&
      selectedDate.value.getFullYear() === year;

    // Randomly assign appointments for demo
    const hasAppointments = Math.random() > 0.7;
    const appointmentCount = hasAppointments
      ? Math.floor(Math.random() * 4) + 1
      : 0;

    dates.push({
      day: i,
      isCurrentMonth: true,
      isToday,
      isSelected,
      hasAppointments,
      appointmentCount,
    });
  }

  // Next month days
  const remainingCells = totalCells - dates.length;
  for (let i = 1; i <= remainingCells; i++) {
    dates.push({
      day: i,
      isCurrentMonth: false,
      isToday: false,
      isSelected: false,
      hasAppointments: false,
      appointmentCount: 0,
    });
  }

  return dates;
});

// Methods
const fetchAppointments = async () => {
  loading.value = true;
  try {
    // Simulate API call
    await new Promise((resolve) => setTimeout(resolve, 500));

    // Mock data
    upcomingAppointments.value = [
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
        serviceType: "Home service",
      },
      {
        id: 3,
        clientName: "Miss Victoria",
        date: "Wed 18, 2024",
        time: "10:00 am",
        serviceType: "Home service",
      },
      {
        id: 4,
        clientName: "Miss Victoria",
        date: "Wed 18, 2024",
        time: "10:00 am",
        serviceType: "Home service",
      },
    ];
  } catch (error) {
    console.error("Failed to fetch appointments:", error);
    upcomingAppointments.value = [];
  } finally {
    loading.value = false;
  }
};

// Lifecycle hooks
onMounted(() => {
  fetchAppointments();
});
</script>
