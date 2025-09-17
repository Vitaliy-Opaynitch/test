<template>
  <header
    class="w-full flex items-center justify-between bg-black text-white px-4 sm:px-6 md:px-10 lg:px-18 py-5 group hover:bg-white transition-colors duration-500"
  >
    <div class="flex items-center gap-4">
      <div class="flex items-center gap-2">
        <HeaderLogo />
        <div
          class="flex flex-col text-sm uppercase tracking-wider transition-colors group-hover:text-black"
        >
          <span>Metadata</span>
          <span>Translation</span>
        </div>
      </div>

      <div class="relative text-xs pl-4 transition-colors group-hover:text-black">
        <span
          class="absolute left-0 top-1/2 transform -translate-y-1/2 h-8 border-l text-[#414141] group-hover:border-black transition-colors"
        ></span>
        Powered by
        <AirMediaTechLogo />
      </div>
    </div>

    <nav
      class="hidden md:flex items-center gap-8 text-sm transition-colors group-hover:text-black whitespace-nowrap"
    >
      <a href="#" class="hover-text-shadow transition-colors">About</a>
      <a href="#" class="hover-text-shadow transition-colors">How it works</a>
      <a href="#" class="hover-text-shadow transition-colors">Cases</a>
      <a href="#" class="hover-text-shadow transition-colors">Pricing</a>
      <a href="#" class="hover-text-shadow transition-colors">FAQ</a>
    </nav>

    <div
      class="flex items-center gap-5 text-[16px] font-semibold transition-colors group-hover:text-black whitespace-nowrap"
    >
      <button class="uppercase group-hover:text-black transition-colors">Login</button>
      <button
        class="border border-white uppercase rounded-md px-[35px] py-2 group-hover:border-black transition-colors"
      >
        Sign Up
      </button>
    </div>
  </header>
</template>

<script setup>
import HeaderLogo from './HeaderLogo.vue'
import AirMediaTechLogo from './AirMediaTechLogo.vue'
</script>

<style scoped>
.hover-text-shadow:hover {
  transition: 0.25s;
  text-shadow: 2px 2px 15px #2e59e7;
}
</style>
