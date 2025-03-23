<template>
  <div v-motion="contactAnimation" class="bg-white rounded-lg p-6">
    <div class="mb-6">
      <h2 class="text-xl font-semibold">Contact Information</h2>
      <p class="text-sm text-gray-500">Input your company contact Information below</p>
    </div>

    <div class="space-y-6">
      <div>
        <div class="flex justify-between items-center mb-1">
          <label class="block text-sm font-medium">Phone Number</label>
          <button class="text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="12" y1="5" x2="12" y2="19"></line>
              <line x1="5" y1="12" x2="19" y2="12"></line>
            </svg>
          </button>
        </div>
        <input 
          type="tel" 
          v-model="contactData.phone" 
          placeholder="Trailblazing" 
          class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
        />
      </div>

      <div>
        <div class="flex justify-between items-center mb-1">
          <label class="block text-sm font-medium">Email address</label>
          <button class="text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="12" y1="5" x2="12" y2="19"></line>
              <line x1="5" y1="12" x2="19" y2="12"></line>
            </svg>
          </button>
        </div>
        <input 
          type="email" 
          v-model="contactData.email" 
          placeholder="Trailblazing" 
          class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
        />
      </div>

      <div>
        <div class="flex justify-between items-center mb-1">
          <label class="block text-sm font-medium">Company Address</label>
          <button class="text-gray-400">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <line x1="12" y1="5" x2="12" y2="19"></line>
              <line x1="5" y1="12" x2="19" y2="12"></line>
            </svg>
          </button>
        </div>
        <textarea 
          v-model="contactData.address" 
          rows="4" 
          placeholder="Write a short description about yourself" 
          class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
        ></textarea>
      </div>

      <!-- Action buttons -->
      <div class="flex justify-end gap-4 mt-8">
        <button 
          @click="resetForm" 
          class="px-6 py-2 border border-gray-300 rounded-md text-red-500 hover:bg-red-50 transition-colors"
        >
          Cancel
        </button>
        <button 
          @click="saveContact" 
          class="px-6 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600 transition-colors"
        >
          Update
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue';

const contactAnimation = {
  initial: { opacity: 0, y: 50 },
  visible: { opacity: 1, y: 0, transition: { duration: 400 } }
};

const contactData = reactive({
  phone: '',
  email: '',
  address: ''
});

const saveContact = () => {
  // Here you would typically send the data to your API
  console.log('Saving contact information:', contactData);
  // Show success message
  alert('Contact information updated successfully!');
};

const resetForm = () => {
  // Reset to initial values or empty the form
  contactData.phone = '';
  contactData.email = '';
  contactData.address = '';
};
</script>