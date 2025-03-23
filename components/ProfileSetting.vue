<template>
  <div v-motion="profileAnimation" class="bg-white rounded-lg p-6">
    <div class="flex flex-col gap-6">
      <!-- Profile picture section -->
      <div class="flex items-center gap-4">
        <div class="relative">
          <div class="w-20 h-20 bg-gray-200 rounded-full flex items-center justify-center overflow-hidden">
            <img v-if="profileImage" :src="profileImage" alt="Profile" class="w-full h-full object-cover" />
            <svg v-else xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-gray-400" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
              <circle cx="12" cy="7" r="4"></circle>
            </svg>
          </div>
        </div>
        <div>
          <h3 class="font-medium">Trailblazing</h3>
          <p class="text-sm text-gray-500">PNG or JPEG</p>
          <button @click="triggerFileInput" class="mt-2 px-4 py-2 border border-gray-300 rounded-md text-sm flex items-center gap-2">
            Upload
            <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"></path>
              <polyline points="17 8 12 3 7 8"></polyline>
              <line x1="12" y1="3" x2="12" y2="15"></line>
            </svg>
          </button>
          <input type="file" ref="fileInput" class="hidden" accept="image/*" @change="handleFileChange" />
        </div>
      </div>

      <!-- Form fields -->
      <div class="space-y-4">
        <div>
          <label class="block text-sm font-medium mb-1">Full Name</label>
          <input 
            type="text" 
            v-model="formData.fullName" 
            placeholder="Trailblazing" 
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
          />
        </div>

        <div>
          <label class="block text-sm font-medium mb-1">Time available</label>
          <input 
            type="text" 
            v-model="formData.timeAvailable" 
            placeholder="Input a period of time you will be available" 
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
          />
        </div>

        <div>
          <label class="block text-sm font-medium mb-1">Address</label>
          <input 
            type="text" 
            v-model="formData.address" 
            placeholder="Lagos, Nigeria" 
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
          />
        </div>

        <div>
          <label class="block text-sm font-medium mb-1">Speciality</label>
          <input 
            type="text" 
            v-model="formData.speciality" 
            placeholder="Input areas you specialise in" 
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
          />
        </div>

        <div>
          <label class="block text-sm font-medium mb-1">Select Service Option you Prefer</label>
          <div class="space-y-2">
            <div class="flex items-center">
              <input 
                type="checkbox" 
                id="homeService" 
                v-model="formData.serviceOptions.homeService" 
                class="h-4 w-4 text-orange-500 focus:ring-orange-500 border-gray-300 rounded"
              />
              <label for="homeService" class="ml-2 text-sm">Home Service</label>
            </div>
            <div class="flex items-center">
              <input 
                type="checkbox" 
                id="saloonService" 
                v-model="formData.serviceOptions.saloonService" 
                class="h-4 w-4 text-orange-500 focus:ring-orange-500 border-gray-300 rounded"
              />
              <label for="saloonService" class="ml-2 text-sm">Saloon Service</label>
            </div>
          </div>
        </div>

        <div>
          <label class="block text-sm font-medium mb-1">Bio</label>
          <textarea 
            v-model="formData.bio" 
            rows="4" 
            placeholder="Write a short description about yourself" 
            class="w-full px-4 py-2 border border-gray-300 rounded-md focus:outline-none focus:ring-2 focus:ring-orange-500"
          ></textarea>
        </div>
      </div>

      <!-- Action buttons -->
      <div class="flex justify-end gap-4 mt-4">
        <button 
          @click="resetForm" 
          class="px-6 py-2 border border-gray-300 rounded-md text-red-500 hover:bg-red-50 transition-colors"
        >
          Cancel
        </button>
        <button 
          @click="saveProfile" 
          class="px-6 py-2 bg-orange-500 text-white rounded-md hover:bg-orange-600 transition-colors"
        >
          Update
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, reactive } from 'vue';

const profileAnimation = {
  initial: { opacity: 0, y: 50 },
  visible: { opacity: 1, y: 0, transition: { duration: 400 } }
};

const fileInput = ref(null);
const profileImage = ref(null);

const formData = reactive({
  fullName: 'Trailblazing',
  timeAvailable: '',
  address: 'Lagos, Nigeria',
  speciality: '',
  serviceOptions: {
    homeService: false,
    saloonService: true
  },
  bio: ''
});

const triggerFileInput = () => {
  fileInput.value.click();
};

const handleFileChange = (event) => {
  const file = event.target.files[0];
  if (file) {
    const reader = new FileReader();
    reader.onload = (e) => {
      profileImage.value = e.target.result;
    };
    reader.readAsDataURL(file);
  }
};

const saveProfile = () => {
  // Here you would typically send the data to your API
  console.log('Saving profile:', formData);
  // Show success message
  alert('Profile updated successfully!');
};

const resetForm = () => {
  // Reset to initial values or empty the form
  formData.fullName = 'Trailblazing';
  formData.timeAvailable = '';
  formData.address = 'Lagos, Nigeria';
  formData.speciality = '';
  formData.serviceOptions.homeService = false;
  formData.serviceOptions.saloonService = true;
  formData.bio = '';
};
</script>