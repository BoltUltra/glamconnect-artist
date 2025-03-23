<script setup lang="ts"></script>

<template>
  <section class="animate-fade-in my-10">
    <div class="my-10 md:px-20 px-5">
      <h3 class="md:text-3xl text-2xl font-bold mb-10">
        A brighter way of booking for beauty
      </h3>
      <div class="flex items-center justify-center">
        <div class="max-w-3xl flex md:flex-row flex-col items-center gap-4">
          <div class="flex flex-col text-center items-center justify-center">
            <img src="/images/payment.svg" alt="" />
            <div class="mt-2 md:px-0 px-20">
              <h5 class="font-semibold text-lg mb-1">Smart Payment</h5>
              <p class="font-light">
                Select from the different ranges of price tag available.
              </p>
            </div>
          </div>
          <div class="flex flex-col text-center items-center justify-center">
            <img src="/images/24.svg" alt="" />
            <div class="mt-2 md:px-0 px-20">
              <h5 class="font-semibold text-lg mb-1">24/7</h5>
              <p class="font-light">
                Book from anywhere at any time of the day
              </p>
            </div>
          </div>
          <div class="flex flex-col text-center items-center justify-center">
            <img src="/images/rating.svg" alt="" />
            <div class="mt-2 md:px-0 px-20">
              <h5 class="font-semibold text-lg mb-1">
                Choose from the top Rating
              </h5>
              <p class="font-light">Thousands of ventures and (Ratings)</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div>
      <div class="md:hidden">
        <div class="bg-[#D1CEAE] rounded-2xl mt-20 pb-10 relative">
          <img src="/images/cta.png" alt="" class="relative -top-14" />
          <div class="bg-white absolute bottom-2 px-5 py-7 rounded-xl">
            <p>
              “A true makeup artist doesn't just enhance features; they reveal
              the unique canvas within every individual. Their artistry lies in
              understanding that beauty is personal, powerful, and
              ever-evolving—transforming not just the face, but the confidence
              and soul behind it.”
            </p>
          </div>
        </div>
        <div class="text-center px-5 py-10">
          <h2 class="text-3xl font-semibold text-gray-900">
            Set up your business on GlamConnect
          </h2>
          <p class="mt-4 text-gray-700">
            Join the largest network of clients searching for top professionals.
          </p>
          <button
            class="mt-6 bg-orange-500 text-white px-6 py-3 rounded-xl hover:bg-orange-600"
          >
            Start your Journey today
          </button>
        </div>
      </div>
      <div class="md:block hidden px-20">
        <div
          class="bg-[#D1CEAE] rounded-2xl mt-20 relative grid grid-cols-2 items-center"
        >
          <div class="relative">
            <img src="/images/cta.png" alt="" class="relative" />
            <div
              class="bg-white dark:text-gray-600 absolute bottom-2 px-5 py-7 rounded-xl mx-5 text-lg"
            >
              <p>
                “A true makeup artist doesn't just enhance features; they reveal
                the unique canvas within every individual. Their artistry lies
                in understanding that beauty is personal, powerful, and
                ever-evolving—transforming not just the face, but the confidence
                and soul behind it.”
              </p>
            </div>
          </div>
          <div class="text-center px-5 py-10">
            <h2 class="text-3xl font-semibold text-gray-900">
              Set up your business on GlamConnect
            </h2>
            <p class="mt-4 text-gray-700 px-20">
              Join the largest network of clients searching for top
              professionals.
            </p>
            <button
              class="mt-6 bg-orange-500 text-white px-6 py-3 rounded-xl hover:bg-orange-600"
            >
              Start your Journey today
            </button>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped></style>
