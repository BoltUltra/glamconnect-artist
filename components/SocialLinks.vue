<template>
  <div v-motion="socialAnimation" class="bg-white rounded-lg p-6">
    <div class="mb-6">
      <h2 class="text-xl font-semibold">Social Media Links</h2>
      <p class="text-sm text-gray-500">Input your company contact Information below</p>
    </div>

    <div class="space-y-6">
      <div v-for="(link, index) in socialLinks" :key="index">
        <div class="flex justify-between items-center mb-1">
          <label class="block text-sm font-medium">{{ link.label }} URL</label>
          <button class="text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="12" y1="5" x2="12" y2="19"></line>
              <line x1="5" y1="12" x2="19" y2="12"></line>
            </svg>
          </button>
        </div>
        <input 
          type="url" 
          v-model="link.value" 
          :placeholder="link.placeholder" 
          class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
        />
      </div>

      <!-- Add more social links button -->
      <button 
        @click="addSocialLink" 
        class="w-full py-3 border border-gray-300 rounded-md flex items-center justify-center gap-2 hover:bg-gray-50 transition-colors"
      >
        <span>Add Social Links</span>
        <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <line x1="12" y1="5" x2="12" y2="19"></line>
          <line x1="5" y1="12" x2="19" y2="12"></line>
        </svg>
      </button>

      <!-- Action buttons (hidden in this view as per design) -->
      <div class="flex justify-end gap-4 mt-8 hidden">
        <button 
          @click="resetForm" 
          class="px-6 py-2 border border-gray-300 rounded-md text-red-500 hover:bg-red-50 transition-colors"
        >
          Cancel
        </button>
        <button 
          @click="saveSocialLinks" 
          class="px-6 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600 transition-colors"
        >
          Update
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const socialAnimation = {
  initial: { opacity: 0, y: 50 },
  visible: { opacity: 1, y: 0, transition: { duration: 400 } }
};

const socialLinks = ref([
  { 
    label: 'Facebook', 
    value: '', 
    placeholder: 'Trailblazing',
    icon: 'facebook'
  },
  { 
    label: 'X', 
    value: '', 
    placeholder: 'Trailblazing',
    icon: 'twitter'
  },
  { 
    label: 'Instagram', 
    value: '', 
    placeholder: 'Trailblazing',
    icon: 'instagram'
  }
]);

const addSocialLink = () => {
  // Add a new custom social link
  socialLinks.value.push({
    label: 'Custom Link',
    value: '',
    placeholder: 'Enter your custom link',
    icon: 'link'
  });
};

const saveSocialLinks = () => {
  // Here you would typically send the data to your API
  console.log('Saving social links:', socialLinks.value);
  // Show success message
  alert('Social links updated successfully!');
};

const resetForm = () => {
  // Reset all social links to empty values
  socialLinks.value.forEach(link => {
    link.value = '';
  });
};
</script>