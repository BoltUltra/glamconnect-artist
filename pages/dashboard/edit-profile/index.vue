<template>
  <div class="flex flex-col min-h-screen">
    <!-- Header -->
    <div class="flex items-center justify-between p-4 md:p-6">
      <div class="flex items-center gap-3">
        <div class="bg-gray-200 rounded-full p-2">
          <Icon
            name="material-symbols:info-outline"
            class="h-5 w-5 text-gray-500"
          />
        </div>
        <div v-motion="headerAnimation">
          <h1 class="text-xl font-bold">Settings</h1>
          <p class="text-sm text-gray-500">
            Manage your preferences and configure various options
          </p>
        </div>
      </div>
      <div class="cursor-pointer">
        <Icon name="material-symbols:notifications-outline" class="h-6 w-6" />
      </div>
    </div>

    <!-- Main content -->
    <TabGroup as="div" class="flex flex-col md:flex-row flex-1 gap-4 p-4">
      <!-- Menu sidebar -->
      <TabList class="w-full md:w-64 bg-white rounded-lg p-4 h-fit space-y-2">
        <h2 class="text-lg font-semibold mb-4">Select menu</h2>
        <Tab
          v-for="item in menuItems"
          :key="item.id"
          v-slot="{ selected }"
          as="template"
        >
          <button
            class="flex items-center w-full gap-2 p-3 rounded-md transition-colors"
            :class="[
              selected
                ? 'bg-orange-50 text-black'
                : 'text-gray-500 hover:bg-gray-100',
            ]"
          >
            <Icon :name="item.icon" class="h-5 w-5" />
            <span>{{ item.label }}</span>
          </button>
        </Tab>
      </TabList>

      <!-- Content area -->
      <TabPanels class="flex-1">
        <TabPanel v-for="item in menuItems" :key="item.id">
          <component
            :is="item.component"
            @show-deactivate-modal="showDeactivateModal = true"
          />
        </TabPanel>
      </TabPanels>
    </TabGroup>

    <!-- Deactivate Account Modal -->
    <DeactivateModal
      v-if="showDeactivateModal"
      @close="showDeactivateModal = false"
    />
  </div>
</template>

<script setup>
import { ref } from "vue";
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from "@headlessui/vue";
import ProfileSetting from "~/components/ProfileSetting.vue";
import ContactInformation from "~/components/ContactInformation.vue";
import SocialLinks from "~/components/SocialLinks.vue";
import AccountSetting from "~/components/AccountSetting.vue";
import DeactivateModal from "~/components/DeactivateModal.vue";

definePageMeta({
  layout: "dashboard",
});

const headerAnimation = {
  initial: { opacity: 0, y: -20 },
  visible: { opacity: 1, y: 0, transition: { duration: 400 } },
};

const showDeactivateModal = ref(false);

const menuItems = [
  {
    id: "profile",
    label: "Profile Setting",
    icon: "material-symbols:person-outline",
    component: ProfileSetting,
  },
  {
    id: "contact",
    label: "Contact Information",
    icon: "material-symbols:contact-mail-outline",
    component: ContactInformation,
  },
  {
    id: "social",
    label: "Social Links",
    icon: "material-symbols:link",
    component: SocialLinks,
  },
  {
    id: "account",
    label: "Account Setting",
    icon: "material-symbols:manage-accounts-outline",
    component: AccountSetting,
  },
];
</script>
