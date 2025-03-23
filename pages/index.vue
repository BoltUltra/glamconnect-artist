<template>
  <div class="max-w-[1440px] mx-auto">
    <Navbar />
    <Hero />
    <WhatWeDo />
    <Recommended />
    <Features />
    <CTA />
  </div>
  <Footer />
</template>

<script setup lang="ts"></script>

<style>
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}
.animate-fade-in {
  animation: fadeIn 1.5s ease-in;
}

@keyframes slideUp {
  from {
    transform: translateY(20px);
    opacity: 0;
  }
  to {
    transform: translateY(0);
    opacity: 1;
  }
}
.animate-slide-up {
  animation: slideUp 1s ease-in-out;
}

@keyframes zoomIn {
  from {
    transform: scale(0.8);
    opacity: 0;
  }
  to {
    transform: scale(1);
    opacity: 1;
  }
}
.animate-zoom-in {
  animation: zoomIn 0.8s ease-in-out;
}
</style>
