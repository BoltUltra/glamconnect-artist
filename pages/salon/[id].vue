<template>
  <main class="max-w-[1440px] mx-auto">
    <Navbar />
    <div class="min-h-screen md:px-20 px-5">
      <!-- Back Button -->
      <NuxtLink to="/" class="flex items-center space-x-2 my-5">
        <Icon name="material-symbols:arrow-left-alt" />
        <span>Back</span>
      </NuxtLink>

      <div class="max-w-4xl mx-auto">
        <!-- Profile Header -->
        <div v-if="salon" class="bg-white rounded-2xl shadow-lg p-6 mb-6">
          <div class="w-16 h-16 bg-gray-200 rounded-full overflow-hidden">
            <img
              :src="salon.avatar"
              alt=""
              class="w-full h-full object-cover"
            />
          </div>
          <div class="flex items-center gap-4 my-6">
            <div>
              <h2 class="text-2xl font-bold">{{ salon.name }}</h2>
              <p class="text-gray-600">
                <Icon name="ic:baseline-pin-drop" /> {{ salon.address }}
              </p>
            </div>
            <button
              class="ml-auto px-6 py-2 bg-orange-500 text-white rounded-lg hover:bg-orange-600 transition-colors"
            >
              Book now
            </button>
          </div>

          <p class="text-gray-700">{{ salon.description }}</p>

          <!-- Rating Section -->
          <div
            class="flex md:flex-row flex-col md:items-center md:justify-between gap-2 mt-5"
          >
            <div class="flex items-center space-x-5 text-blue-500">
              <a :href="salon.facebook" target="_blank">
                <Icon name="fa-brands:facebook" class="w-6 h-6 mr-2" />
                <span>{{ salon.facebook }}</span>
              </a>
              <a :href="salon.instagram" target="_blank">
                <Icon name="fa-brands:instagram" class="w-6 h-6 mr-2" />
                <span>{{ salon.instagram }}</span>
              </a>
            </div>
            <div class="flex items-center gap-2">
              <span>Ratings</span>
              <div class="flex">
                <svg
                  v-for="i in 5"
                  :key="i"
                  class="w-5 h-5 text-yellow-400"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                >
                  <path
                    d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z"
                  />
                </svg>
              </div>
            </div>
          </div>
        </div>

        <!-- Portfolio Section -->
        <div v-if="salon" class="bg-white rounded-2xl shadow-lg p-6">
          <h3 class="text-xl font-semibold mb-4">Portfolio</h3>
          <div class="grid grid-cols-2 md:grid-cols-3 gap-4">
            <div
              v-for="(image, index) in salon.portfolio"
              :key="index"
              class="aspect-square rounded-lg overflow-hidden"
            >
              <img
                :src="image"
                alt=""
                class="w-full h-full object-cover hover:scale-105 transition-transform duration-300"
              />
            </div>
          </div>
        </div>
      </div>
    </div>
    <Footer />
  </main>
</template>

<script setup>
const route = useRoute();
const salon = {
  name: "Glamour Hub",
  address: "456 Style Avenue",
  avatar: "/images/user.svg",
  description:
    "Hi, I’m Trailblazing, a professional makeup artist with over 2 years of experience specializing in bridal, editorial, and event makeup. My passion is enhancing natural beauty while creating unique, personalized looks for each client. Whether you're looking for soft glam or bold, creative artistry, I'm here to make sure you feel confident and radiant on your special day",
  rating: 4.5,
  reviews: 98,
  facebook: "https://facebook.com",
  instagram: "https://instagram.com",
  portfolio: [
    "/images/img1.webp",
    "/images/img2.webp",
    "/images/img3.webp",
    "/images/img4.webp",
    "/images/img2.webp",
    "/images/img1.webp",
    "/images/img4.webp",
    "/images/img2.webp",
    "/images/img3.webp",
  ],
};
</script>
