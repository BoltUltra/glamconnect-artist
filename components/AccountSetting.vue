<template>
  <div v-motion="accountAnimation" class="bg-white rounded-lg p-6">
    <div class="mb-6">
      <h2 class="text-xl font-semibold">Account Setting</h2>
      <p class="text-sm text-gray-500">Take control of your account</p>
    </div>

    <div class="space-y-8">
      <!-- Change Password Section -->
      <div>
        <h3 class="text-lg font-medium mb-1">Change Password</h3>
        <p class="text-sm text-gray-500 mb-4">Take control of your account</p>

        <div class="space-y-4">
          <div>
            <label class="block text-sm font-medium mb-1">Input a New password</label>
            <input 
              type="password" 
              v-model="passwordData.newPassword" 
              placeholder="Trailblazing" 
              class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
            />
          </div>

          <div>
            <label class="block text-sm font-medium mb-1">Confirm Password</label>
            <input 
              type="password" 
              v-model="passwordData.confirmPassword" 
              placeholder="Trailblazing" 
              class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
            />
          </div>
        </div>

        <div class="mt-6">
          <button 
            @click="updatePassword" 
            class="px-6 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600 transition-colors"
          >
            Update
          </button>
        </div>
      </div>

      <!-- Deactivate Account Section -->
      <div class="pt-4">
        <button 
          @click="showDeactivateConfirm" 
          class="flex items-center gap-2 text-red-500 hover:text-red-600 transition-colors"
        >
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M13 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2v-9"></path>
            <path d="M18 9V4a1 1 0 0 0-1-1h-4"></path>
            <path d="m9 15 3-3 3 3"></path>
            <path d="M12 12v6"></path>
          </svg>
          <span>Deactivate Account</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { reactive } from 'vue';

const accountAnimation = {
  initial: { opacity: 0, y: 50 },
  visible: { opacity: 1, y: 0, transition: { duration: 400 } }
};

const passwordData = reactive({
  newPassword: '',
  confirmPassword: ''
});

const emit = defineEmits(['show-deactivate-modal']);

const updatePassword = () => {
  if (passwordData.newPassword !== passwordData.confirmPassword) {
    alert('Passwords do not match!');
    return;
  }
  
  if (passwordData.newPassword.length < 6) {
    alert('Password must be at least 6 characters long');
    return;
  }
  
  // Here you would typically send the data to your API
  console.log('Updating password:', passwordData);
  // Show success message
  alert('Password updated successfully!');
  
  // Reset form
  passwordData.newPassword = '';
  passwordData.confirmPassword = '';
};

const showDeactivateConfirm = () => {
  emit('show-deactivate-modal');
};
</script>