<template>
  <header
    :class="[
      'sticky top-0 z-50 w-full flex items-center justify-between px-4 sm:px-6 md:px-10 lg:px-18 py-5 transition-colors duration-500',
      isLight ? 'bg-white text-black' : 'bg-black text-white',
    ]"
  >
    <div class="flex items-center gap-4">
      <div class="flex items-center gap-2">
        <HeaderLogo :class="[isLight ? '!text-black' : '!text-white']" />
        <div class="flex flex-col text-sm uppercase tracking-wider transition-colors">
          <span>Metadata</span>
          <span>Translation</span>
        </div>
      </div>

      <div class="relative text-xs pl-4 transition-colors">
        <span
          class="absolute left-0 top-1/2 transform -translate-y-1/2 h-8 border-l text-[#414141]"
        ></span>
        Powered by
        <AirMediaTechLogo :class="[isLight ? '!text-black' : '!text-white']" />
      </div>
    </div>

    <nav class="hidden md:flex items-center gap-8 text-sm transition-colors whitespace-nowrap">
      <a href="#" class="hover-text-shadow transition-colors">About</a>
      <a href="#" class="hover-text-shadow transition-colors">How it works</a>
      <a href="#" class="hover-text-shadow transition-colors">Cases</a>
      <a href="#" class="hover-text-shadow transition-colors">Pricing</a>
      <a href="#" class="hover-text-shadow transition-colors">FAQ</a>
    </nav>

    <div
      class="flex items-center gap-5 text-[16px] font-semibold transition-colors whitespace-nowrap"
    >
      <button class="uppercase">Login</button>
      <button
        class="sign-up-button"
        :class="isLight ? 'sign-up-button--light' : 'sign-up-button--dark'"
      >
        <span
          class="sign-up-button__btn-label"
          :class="[
            isLight ? 'sign-up-button__btn-label--black' : 'sign-up-button__btn-label--white',
          ]"
          >Sign Up</span
        >
      </button>
    </div>
  </header>
</template>

<script setup>
import HeaderLogo from './HeaderLogo.vue'
import AirMediaTechLogo from './AirMediaTechLogo.vue'

defineProps({
  isLight: {
    type: Boolean,
    default: false,
  },
})
</script>

<style scoped>
.hover-text-shadow:hover {
  transition: 0.25s;
  text-shadow: 2px 2px 15px #003cff;
}

.sign-up-button {
  position: relative;
  overflow: hidden;
  text-transform: uppercase;
  border-radius: 0.375rem;
  padding: 0.5rem 35px;
  border: 1px solid currentColor;
  color: inherit;
  transition:
    color 0.3s ease,
    border-color 0.3s ease;
}

.sign-up-button::before {
  content: '';
  position: absolute;
  inset: 0;
  background: currentColor;
  border-radius: inherit;
  transform: scaleX(0);
  transform-origin: left center;
  z-index: 1;
  transition: transform 0.6s cubic-bezier(0.22, 0.9, 0.3, 1);
}

.sign-up-button:hover::before {
  transform: scaleX(1);
}

.sign-up-button__btn-label {
  position: relative;
  z-index: 2;
  transition: color 0.3s ease;
}

.sign-up-button:hover .sign-up-button__btn-label--black {
  color: #fff;
}

.sign-up-button:hover .sign-up-button__btn-label--white {
  color: #000;
}
</style>
