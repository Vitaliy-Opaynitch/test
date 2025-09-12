<template>
  <AppHeader />
  <AppHero />
  <p>
    Visit <a href="https://vuejs.org/" target="_blank" rel="noopener">vuejs.org</a> to read the
    documentation
  </p>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import AppHeader from './components/Header/AppHeader.vue'
import AppHero from './components/Hero/AppHero.vue'

const box = ref(null)

onMounted(() => {
  gsap.to(box.value, {
    x: 200,
    rotation: 360,
    duration: 2,
    ease: 'power2.inOut',
  })
})
</script>

<style scoped></style>
