<script setup></script>

<template>
  <footer
    class="bg-[#E7E7E7] md:px-20 px-5 relative py-20 text-[#5D6474] max-w-[1440px] mx-auto"
  >
    <div class="">
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-5 gap-8">
        <!-- Logo and Social Section -->
        <div class="space-y-6 lg:col-span-2">
          <div class="flex-shrink-0">
            <img class="w-32 h-7" src="/images/logo.png" alt="Logo" />
          </div>
        </div>

        <!-- Company Section -->
        <div>
          <h3 class="text-lg font-semibold mb-4">Company</h3>
          <ul class="space-y-2">
            <li>
              <a href="#" class="hover:text-primary-500 transition-colors"
                >About</a
              >
            </li>
            <li>
              <a href="#" class="hover:text-primary-500 transition-colors"
                >Help and Support</a
              >
            </li>
          </ul>
        </div>

        <!-- Help Section -->
        <div>
          <h3 class="text-lg font-semibold mb-4">Contact</h3>
          <ul class="space-y-2">
            <li>
              <Icon name="mynaui:envelope" />
              <a
                href="mailto:vickygideon@gmail.com"
                class="hover:text-primary-500 transition-colors hover:underline underline-offset-4"
              >
                vickygideon@gmail.com
              </a>
            </li>
            <li>
              <Icon name="material-symbols-light:phone-in-talk" />
              <a
                href="tel:+2349010825406"
                class="hover:text-primary-500 transition-colors hover:underline underline-offset-4"
              >
                +234 901 082 5406
              </a>
            </li>
            <li>
              <Icon name="ic:baseline-pin-drop" />
              <p class="inline-block pl-2">Lagos, Nigeria.</p>
            </li>
          </ul>
        </div>

        <!-- Newsletter Section -->
        <div>
          <h3 class="text-lg font-semibold mb-4">Social Media</h3>
          <div class="flex space-x-3">
            <a href="#" class="">
              <Icon name="line-md:facebook" size="18" />
            </a>
            <a href="#" class="">
              <Icon name="line-md:instagram" size="18" />
            </a>
            <a href="#" class="">
              <Icon name="line-md:youtube" size="18" />
            </a>
            <a href="#" class="">
              <Icon name="line-md:twitter-x" size="18" />
            </a>
          </div>
        </div>
      </div>

      <!-- Copyright -->
      <div class="mt-12 pt-8 border-t border-gray-600 text-center text-sm z-10">
        Copyright © 2023 TTS Software Company | All Rights Reserved
      </div>
      <img src="/images/footer.png" alt="" class="absolute bottom-0 left-0" />
    </div>
  </footer>
</template>
