<template>
  <div class="flex min-h-screen bg-gray-100">
    <AppSidebar
      :default-collapsed="isSidebarCollapsed"
      @collapse-change="handleSidebarCollapse"
    />

    <!-- Main Content -->
    <main
      class="flex-1 p-6 transition-all duration-300 ease-in-out"
      :class="[isSidebarCollapsed ? 'md:ml-16' : 'md:ml-64']"
    >
      <NuxtPage />
    </main>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";
import { Menu } from "lucide-vue-next";

const isSidebarCollapsed = ref(false);

const handleSidebarCollapse = (collapsed) => {
  isSidebarCollapsed.value = collapsed;
};

const toggleMobileSidebar = () => {
  isSidebarCollapsed.value = !isSidebarCollapsed.value;
};

onMounted(() => {
  if (process.client) {
    const savedState = localStorage.getItem("sidebarCollapsed");
    if (savedState !== null) {
      isSidebarCollapsed.value = savedState === "true";
    }
  }
});
</script>
