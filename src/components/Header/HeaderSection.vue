<template>
  <header
    ref="headerRef"
    :class="[
      'sticky top-0 z-50 w-full flex items-center justify-between px-4 sm:px-6 md:px-10 lg:px-18 py-5 transition-colors duration-500',
      isLight ? 'bg-white text-black' : 'bg-black text-white',
    ]"
  >
    <!-- Logo Section -->
    <div class="flex items-center gap-4">
      <div class="flex items-center gap-2">
        <HeaderLogo :class="[isLight ? '!text-black' : '!text-white']" />
        <div class="flex flex-col text-sm uppercase tracking-wider transition-colors">
          <span>Metadata</span>
          <span>Translation</span>
        </div>
      </div>

      <div class="relative text-xs pl-4 transition-colors">
        <span class="absolute left-0 top-1/2 -translate-y-1/2 h-8 border-l border-[#414141]"></span>
        Powered by
        <AirMediaTechLogo :class="[isLight ? '!text-black' : '!text-white']" />
      </div>
    </div>

    <!-- Navigation -->
    <nav class="hidden md:flex items-center gap-8 text-sm transition-colors whitespace-nowrap">
      <a
        v-for="link in navigationLinks"
        :key="link.name"
        :href="link.href"
        class="hover-text-shadow transition-colors"
      >
        {{ link.name }}
      </a>
    </nav>

    <!-- Action Buttons -->
    <div
      class="flex items-center gap-5 text-base font-semibold transition-colors whitespace-nowrap"
    >
      <button class="uppercase">Login</button>
      <button ref="signUpButtonRef" class="sign-up-button">
        <span
          class="sign-up-button__btn-label"
          :class="[
            isLight ? 'sign-up-button__btn-label--black' : 'sign-up-button__btn-label--white',
          ]"
        >
          Sign Up
        </span>
      </button>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import HeaderLogo from './HeaderLogo.vue'
import AirMediaTechLogo from './AirMediaTechLogo.vue'

defineProps({
  isLight: {
    type: Boolean,
    default: false,
  },
})

// Refs for GSAP animations
const headerRef = ref(null)
const signUpButtonRef = ref(null)

// Navigation data
const navigationLinks = [
  { name: 'About', href: '#' },
  { name: 'How it works', href: '#' },
  { name: 'Cases', href: '#' },
  { name: 'Pricing', href: '#' },
  { name: 'FAQ', href: '#' },
]

// GSAP timeline for header animations
let headerTimeline

onMounted(() => {
  // Create GSAP timeline for header entrance animation
  headerTimeline = gsap.timeline({ delay: 0.2 })

  if (headerRef.value) {
    headerTimeline
      .from(headerRef.value, {
        y: -100,
        opacity: 0,
        duration: 0.8,
        ease: 'power3.out',
      })
      .from(
        headerRef.value.querySelectorAll('a, button'),
        {
          y: 20,
          opacity: 0,
          duration: 0.6,
          stagger: 0.1,
          ease: 'power2.out',
        },
        '-=0.4',
      )
  }
})
</script>

<style scoped>
.hover-text-shadow:hover {
  transition: 0.25s;
  text-shadow: 2px 2px 15px #003cff;
}

.login-button {
  background: transparent;
  border: none;
  cursor: pointer;
  font-weight: inherit;
  font-size: inherit;
  transition: opacity 0.3s ease;
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
