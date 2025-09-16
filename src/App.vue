<template>
  <AppHeader />
  <AppHero />
  <QuestionBlock />
  <ForecastBlock />
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { gsap } from 'gsap'
import AppHeader from './components/Header/AppHeader.vue'
import AppHero from './components/Hero/AppHero.vue'
import QuestionBlock from './components/QuestionBlock.vue'
import ForecastBlock from './components/ForecastBlock.vue'

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
