<template>
  <!-- Mobile Toggle Button -->
  <button
    class="fixed top-4 left-4 z-50 md:hidden bg-white p-2 rounded-md shadow-md"
    @click="isOpen = true"
    aria-label="Open menu"
  >
    <Menu class="w-6 h-6" />
  </button>

  <!-- Backdrop Overlay (Mobile) -->
  <div
    v-if="isOpen"
    class="fixed inset-0 bg-black/50 z-40 md:hidden"
    @click="isOpen = false"
  ></div>

  <!-- Sidebar Container -->
  <aside
    class="fixed inset-y-0 left-0 z-40 flex flex-col h-full bg-white border-r border-gray-200 transition-all duration-300 ease-in-out"
    :class="[
      // Mobile: Full width when open, hidden when closed
      isOpen ? 'translate-x-0 w-[280px]' : '-translate-x-full',
      // Desktop: Fixed width based on collapsed state, always visible
      'md:translate-x-0 md:block',
      isCollapsed ? 'md:w-20' : 'md:w-64',
    ]"
  >
    <!-- Sidebar Header -->
    <div
      class="flex items-center justify-between h-16 px-4 border-b border-gray-200"
    >
      <h1
        class="text-xl font-bold truncate transition-opacity duration-300"
        :class="{ 'opacity-0 md:opacity-0': isCollapsed }"
      >
        GlamConnect
      </h1>
      <div class="flex">
        <!-- Mobile Close Button -->
        <button
          @click="isOpen = false"
          class="p-1 rounded-full hover:bg-gray-100 md:hidden"
          aria-label="Close sidebar"
        >
          <ChevronLeft class="w-6 h-6" />
        </button>

        <!-- Desktop Toggle Button -->
        <button
          @click="toggleCollapse"
          class="hidden md:block p-1 rounded-full hover:bg-gray-100"
          aria-label="Toggle sidebar"
        >
          <ChevronLeft v-if="!isCollapsed" class="w-5 h-5" />
          <ChevronRight v-else class="w-5 h-5" />
        </button>
      </div>
    </div>

    <!-- Navigation Links -->
    <nav class="flex-1 overflow-y-auto">
      <ul class="p-2 space-y-1">
        <li v-for="(item, index) in navItems" :key="index">
          <!-- Regular Nav Item -->
          <template v-if="!item.children">
            <div class="flex w-full items-center">
              <div
                :class="{
                  'bg-orange-600 w-1 h-8 rounded-r-3xl':
                    route.path === item.path,
                }"
              ></div>
              <NuxtLink
                :to="item.path"
                class="flex items-center px-4 py-2 text-gray-700 hover:bg-orange-50 rounded-lg transition-colors duration-200 w-full"
                :class="{
                  'bg-orange-100 text-orange-600': route.path === item.path,
                  'justify-center': isCollapsed,
                }"
                @click="isOpen = false"
              >
                <component
                  :is="item.icon"
                  :class="[isCollapsed ? 'w-5 h-5' : 'w-5 h-5 mr-3']"
                />
                <span
                  v-if="!isCollapsed"
                  class="transition-opacity duration-200 whitespace-nowrap"
                >
                  {{ item.name }}
                </span>
              </NuxtLink>
            </div>
          </template>

          <!-- Dropdown Nav Item -->
          <template v-else>
            <div class="flex w-full items-center">
              <div
                :class="{
                  'bg-orange-600 w-1 h-8 rounded-r-3xl':
                    route.path === item.path || isActive(item),
                }"
              ></div>

              <div class="flex flex-col w-full">
                <!-- Parent Item -->
                <NuxtLink
                  :to="item.path"
                  class="flex items-center px-4 py-2 text-gray-700 hover:bg-orange-50 rounded-lg transition-colors duration-200 w-full"
                  :class="{
                    'bg-orange-100 text-orange-600':
                      route.path === item.path || isActive(item),
                    'justify-center': isCollapsed,
                  }"
                  @click="toggleDropdown(item)"
                >
                  <div class="flex items-center justify-between w-full">
                    <div class="flex items-center">
                      <component
                        :is="item.icon"
                        :class="[isCollapsed ? 'w-5 h-5' : 'w-5 h-5 mr-3']"
                      />
                      <span
                        v-if="!isCollapsed"
                        class="transition-opacity duration-200 whitespace-nowrap"
                      >
                        {{ item.name }}
                      </span>
                    </div>
                    <ChevronDown
                      v-if="!isCollapsed"
                      class="w-4 h-4 transition-transform duration-200 ml-2"
                      :class="{ 'rotate-180': isDropdownOpen(item) }"
                    />
                  </div>
                </NuxtLink>

                <!-- Children Items -->
                <ul
                  v-if="!isCollapsed && isDropdownOpen(item)"
                  class="mt-1 space-y-1 pl-6"
                >
                  <li v-for="child in item.children" :key="child.path">
                    <NuxtLink
                      :to="child.path"
                      class="flex items-center px-4 py-2 text-sm text-gray-600 hover:bg-orange-50 rounded-lg transition-colors duration-200"
                      :class="{
                        'bg-orange-100 text-orange-600':
                          route.path === child.path,
                      }"
                      @click="isOpen = false"
                    >
                      <component :is="child.icon" class="w-4 h-4 mr-2" />
                      <span class="whitespace-nowrap">{{ child.name }}</span>
                    </NuxtLink>
                  </li>
                </ul>
              </div>
            </div>
          </template>
        </li>
      </ul>
    </nav>

    <!-- Sidebar Footer -->
    <div class="p-4 border-t border-gray-200">
      <NuxtLink
        to="/logout"
        class="flex items-center text-red-600 hover:bg-red-50 rounded-lg px-4 py-2 transition-colors duration-200"
        :class="{ 'justify-center': isCollapsed }"
        @click="isOpen = false"
      >
        <LogOut :class="[isCollapsed ? 'w-5 h-5' : 'w-5 h-5 mr-3']" />
        <span v-if="!isCollapsed" class="transition-opacity duration-200">
          Sign out
        </span>
      </NuxtLink>
    </div>
  </aside>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";
import {
  LayoutDashboard,
  User,
  CalendarRange,
  Star,
  Calendar,
  RotateCw,
  Settings,
  HelpCircle,
  LogOut,
  ChevronLeft,
  ChevronRight,
  ChevronDown,
  Menu,
} from "lucide-vue-next";

const props = defineProps({
  defaultCollapsed: {
    type: Boolean,
    default: false,
  },
});

const emit = defineEmits(["collapse-change"]);

const route = useRoute();
const isCollapsed = ref(props.defaultCollapsed);
const isOpen = ref(false);
const openDropdowns = ref([]);

const navItems = [
  { name: "Dashboard", path: "/dashboard", icon: LayoutDashboard },
  { name: "User Profile", path: "/dashboard/profile", icon: User },
  {
    name: "Booking Management",
    path: "/dashboard/bookings",
    icon: CalendarRange,
    children: [
      { name: "Live Review", path: "/dashboard/bookings/reviews", icon: Star },
      {
        name: "Appointment Request",
        path: "/dashboard/bookings/appointment-request",
        icon: Calendar,
      },
      {
        name: "Appointment History",
        path: "/dashboard/bookings/appointment-history",
        icon: RotateCw,
      },
    ],
  },
  { name: "Edit profile", path: "/dashboard/edit-profile", icon: Settings },
  { name: "Help and Support", path: "/dashboard/support", icon: HelpCircle },
];

const toggleCollapse = () => {
  isCollapsed.value = !isCollapsed.value;
  if (process.client) {
    localStorage.setItem("sidebarCollapsed", isCollapsed.value.toString());
  }
  emit("collapse-change", isCollapsed.value);
};

const toggleDropdown = (item) => {
  const index = openDropdowns.value.indexOf(item.name);
  if (index > -1) {
    openDropdowns.value.splice(index, 1);
  } else {
    openDropdowns.value.push(item.name);
  }
};

const isDropdownOpen = (item) => {
  return openDropdowns.value.includes(item.name);
};

const isActive = (item) => {
  if (!item.children) return false;
  return item.children.some((child) => route.path === child.path);
};

onMounted(() => {
  if (process.client) {
    const savedState = localStorage.getItem("sidebarCollapsed");
    if (savedState !== null) {
      isCollapsed.value = savedState === "true";
    }
  }
});
</script>
