<template>
  <div 
    v-motion="modalBackdropAnimation"
    class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50"
    @click="closeOnBackdrop"
  >
    <div 
      v-motion="modalAnimation"
      class="bg-white rounded-lg p-6 w-full max-w-md mx-4 shadow-xl" 
      @click.stop
    >
      <div class="text-center mb-6">
        <h3 class="text-lg font-medium">Are you sure you want deactivate account?</h3>
      </div>
      
      <div class="flex justify-center gap-4">
        <button 
          @click="$emit('close')" 
          class="px-6 py-2 border border-gray-300 rounded-md hover:bg-gray-50 transition-colors"
        >
          Cancel
        </button>
        <button 
          @click="deactivateAccount" 
          class="px-6 py-2 bg-red-500 text-white rounded-md hover:bg-red-600 transition-colors"
        >
          Deactivate
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['close']);

const modalBackdropAnimation = {
  initial: { opacity: 0 },
  visible: { opacity: 1, transition: { duration: 200 } },
  leave: { opacity: 0, transition: { duration: 200 } }
};

const modalAnimation = {
  initial: { opacity: 0, scale: 0.9 },
  visible: { opacity: 1, scale: 1, transition: { duration: 300 } },
  leave: { opacity: 0, scale: 0.9, transition: { duration: 200 } }
};

const closeOnBackdrop = (event) => {
  if (event.target === event.currentTarget) {
    emit('close');
  }
};

const deactivateAccount = () => {
  // Here you would typically send the request to deactivate the account
  console.log('Deactivating account...');
  // Show success message and redirect
  alert('Your account has been deactivated');
  // Redirect to login or home page
  // navigateTo('/login');
  emit('close');
};
</script>