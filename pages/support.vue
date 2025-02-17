<template>
  <Navbar />
  <div class="max-w-[1440px] mx-auto md:px-20 px-5 py-20">
    <button class="flex items-center text-gray-600 mb-6">
      <span class="mr-2">&#8592;</span> Back
    </button>

    <div class="grid md:grid-cols-3 gap-6">
      <div class="p-4">
        <div class="flex items-center space-x-3 mb-5">
          <img src="/images/getting-started.svg" alt="" />
          <h2 class="font-semibold">Getting Started</h2>
        </div>
        <div class="text-gray-600 text-sm space-y-4">
          <li>How to create an account</li>
          <li>Browsing and booking a makeup artist</li>
          <li>Payment process and refunds</li>
        </div>
      </div>

      <div class="p-4">
        <div class="flex items-center space-x-3 mb-5">
          <img src="/images/troubleshooting.svg" alt="" />
          <h2 class="font-semibold">Troubleshooting</h2>
        </div>
        <h3 class="font-medium text-gray-700">Account Issues</h3>
        <div class="text-gray-600 text-sm space-y-4 mb-5 mt-3">
          <li>Resetting passwords</li>
          <li>Update account details</li>
        </div>
        <h3 class="font-medium text-gray-700">Booking Issues</h3>
        <div class="text-gray-600 text-sm space-y-4 mt-3">
          <li>Cannot confirm a booking</li>
          <li>Problems with payment processing</li>
        </div>
      </div>

      <div class="p-4">
        <div class="flex items-center space-x-3 mb-5">
          <img src="/images/policies.svg" alt="" />
          <h2 class="font-semibold">Policies and Guidelines</h2>
        </div>
        <div class="text-gray-600 text-sm space-y-4">
          <li>Cancellations and refund policy</li>
          <li>Community guidelines for artists</li>
          <li>Safety and Privacy Policy</li>
        </div>
      </div>

      <div>
        <div class="mt-10">
          <h3 class="font-semibold text-lg">Contact Us</h3>
          <button
            class="bg-orange-500 text-white px-4 py-2 rounded-xl mt-2 md:w-3/4 w-full"
          >
            Start Live Chat
          </button>
        </div>

        <div class="mt-6 text-right">
          <h3 class="font-semibold text-lg text-left">
            Submit suggestions for platform improvement
          </h3>
          <textarea
            class="w-full mt-2 p-3 rounded-xl focus:outline-none focus:ring-2 focus:ring-orange-400 bg-[#F6F6F6]"
            rows="4"
            placeholder="Write a suggestion..."
          ></textarea>
          <button
            class="bg-orange-500 text-white px-4 py-2 rounded-xl mt-2 md:w-2/4 w-full"
          >
            Submit
          </button>
        </div>
      </div>
    </div>
  </div>
  <Footer />
</template>

<script setup>
// Nuxt 3 setup script, no additional logic required for static content
</script>

<style scoped>
/* Additional styles if needed */
</style>
