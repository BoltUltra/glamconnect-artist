<template>
  <div class="p-4 md:p-6 max-w-6xl">
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
            d="M15.9999 23.1666C12.318 23.1666 9.33325 20.1818 9.33325 16.4999C9.33325 12.818 12.318 9.83325 15.9999 9.83325C19.6818 9.83325 22.6666 12.818 22.6666 16.4999C22.6666 20.1818 19.6818 23.1666 15.9999 23.1666ZM15.3333 18.4999V19.8333H16.6666V18.4999H15.3333ZM16.6666 17.4033C17.6304 17.1165 18.3333 16.2236 18.3333 15.1666C18.3333 13.8779 17.2886 12.8333 15.9999 12.8333C14.8679 12.8333 13.9242 13.6394 13.7115 14.7089L15.0191 14.9704C15.1103 14.5121 15.5148 14.1666 15.9999 14.1666C16.5522 14.1666 16.9999 14.6143 16.9999 15.1666C16.9999 15.7189 16.5522 16.1666 15.9999 16.1666C15.6317 16.1666 15.3333 16.4651 15.3333 16.8333V17.8333H16.6666V17.4033Z"
            fill="#5D6474"
          />
        </svg>
      </div>
      <div class="">
        <h1 class="text-2xl font-bold">Help and Support</h1>
        <p class="text-gray-600 text-sm">What can we help you with?</p>
      </div>
    </div>

    <div class="grid md:grid-cols-2 gap-6">
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
            class="w-full mt-2 p-3 rounded-xl focus:outline-none focus:ring-2 focus:ring-orange-400 bg-[#F6F6F6] border"
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
</template>

<script setup></script>

<style scoped></style>
