<template>
  <header class="bg-black text-white border-b border-neutral-800">
    <div class="container mx-auto flex items-center justify-between px-6 py-4">
      <div class="flex items-center gap-6">
        <div class="flex items-center gap-2">
          <!-- Logo (замінити на свій svg/img) -->
          <img :src="aiLogo" alt="AI Metadata Translation" class="h-8 w-auto" />
          <span class="text-sm uppercase tracking-wider">Metadata Translation</span>
        </div>

        <div class="text-xs text-gray-400">
          Powered by
          <img :src="mediaTechLogo" alt="Air Media Tech" class="h-8 w-auto" />
        </div>
      </div>

      <!-- Center: Navigation -->
      <nav class="hidden md:flex items-center gap-8 text-sm">
        <a href="#" class="hover:text-gray-300 transition-colors">About</a>
        <a href="#" class="hover:text-gray-300 transition-colors">How it works</a>
        <a href="#" class="hover:text-gray-300 transition-colors">Cases</a>
        <a href="#" class="hover:text-gray-300 transition-colors">Pricing</a>
        <a href="#" class="hover:text-gray-300 transition-colors">FAQ</a>
      </nav>

      <!-- Right: Auth buttons -->
      <div class="flex items-center gap-4">
        <button class="text-sm hover:text-gray-300 transition-colors">Login</button>
        <button
          class="border border-white rounded-md px-4 py-2 text-sm font-semibold hover:bg-white hover:text-black transition-colors"
        >
          Sign Up
        </button>
      </div>
    </div>
  </header>
</template>

<script setup>
import aiLogo from '../assets/ai-logo.svg'
import mediaTechLogo from '../assets/media_tech_logo.svg'
</script>

<style scoped>
.container {
  max-width: 1200px;
}
</style>
