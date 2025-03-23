<script setup>
import { ref } from "vue";
import { Menu, X } from "lucide-vue-next";

const isOpen = ref(false);

const toggleMenu = () => {
  isOpen.value = !isOpen.value;
};

const navItems = [
  { name: "Contact Us", href: "/#contact" },
  { name: "About Us", href: "/#about" },
  { name: "Our Services", href: "/#services" },
];
</script>

<template>
  <nav class="bg-white dark:bg-gray-800 py-6 transition__custom">
    <div class="container__custom md:py-4">
      <div class="flex items-center justify-between">
        <NuxtLink href="/" class="flex-shrink-0">
          <img class="w-32 h-7 dark:invert" src="/images/logo.png" alt="Logo" />
        </NuxtLink>
        <div class="flex items-center">
          <div class="hidden lg:block">
            <div class="ml-10 flex items-baseline space-x-4">
              <NuxtLink
                v-for="item in navItems"
                :key="item.name"
                :href="item.href"
                class="text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700 px-3 py-2 rounded-md text-sm font-medium"
              >
                {{ item.name }}
              </NuxtLink>
            </div>
          </div>
        </div>

        <div class="hidden lg:flex items-center space-x-3">
          <ThemeToggle />
          <!--          <div class="flex items-center space-x-3">-->
          <!--            <NuxtLink-->
          <!--              href="/auth/register"-->
          <!--              class="bg-white py-3 px-14 rounded-2xl text-primary-500 border border-primary-500"-->
          <!--            >-->
          <!--              Sign Up-->
          <!--            </NuxtLink>-->
          <!--            <NuxtLink-->
          <!--              href="/auth/login"-->
          <!--              class="bg-primary-500 py-3 px-16 rounded-2xl text-white border border-primary-500"-->
          <!--            >-->
          <!--              Sign In-->
          <!--            </NuxtLink>-->
          <!--          </div>-->
          <div class="flex items-center space-x-3">
            <NuxtLink
              href="/user-type"
              class="bg-primary-500 py-3 px-16 rounded-2xl text-white border border-primary-500"
            >
              Get Started
            </NuxtLink>
          </div>
        </div>
        <div class="-mr-2 flex lg:hidden">
          <ThemeToggle />
          <button
            @click="toggleMenu"
            type="button"
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-700 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white hover:bg-gray-100 dark:hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white"
            aria-controls="mobile-menu"
            :aria-expanded="isOpen"
          >
            <span class="sr-only">Open main menu</span>
            <Menu v-if="!isOpen" class="block h-6 w-6" aria-hidden="true" />
            <X v-else class="block h-6 w-6" aria-hidden="true" />
          </button>
        </div>
      </div>
    </div>

    <div
      class="lg:hidden"
      id="mobile-menu"
      :class="{ block: isOpen, hidden: !isOpen }"
    >
      <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
        <a
          v-for="item in navItems"
          :key="item.name"
          :href="item.href"
          class="text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-700 block px-3 py-2 rounded-md text-base font-medium"
        >
          {{ item.name }}
        </a>
      </div>
      <div class="flex items-center space-x-3 text-center px-3">
        <NuxtLink
          href="/auth/register"
          class="bg-white py-3 w-full rounded-2xl text-primary-500 border border-primary-500"
        >
          Sign Up
        </NuxtLink>
        <NuxtLink
          href="/auth/login"
          class="bg-primary-500 py-3 w-full rounded-2xl text-white border border-primary-500"
        >
          Sign In
        </NuxtLink>
      </div>
    </div>
  </nav>
</template>
