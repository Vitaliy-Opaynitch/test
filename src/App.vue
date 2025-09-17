<template>
  <HeaderSection :isLight="isLightHeader" />
  <HeroSection :ref="(el) => el && sections.push(el)" />
  <QuestionSection :ref="(el) => el && sections.push(el)" class="light-section" />
  <ForecastSection :ref="(el) => el && sections.push(el)" />
  <StepsSection :ref="(el) => el && sections.push(el)" class="light-section" />
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import HeaderSection from './components/Header/HeaderSection.vue'
import HeroSection from './components/Hero/HeroSection.vue'
import QuestionSection from './components/QuestionSection.vue'
import ForecastSection from './components/ForecastSection.vue'
import StepsSection from './components/StepsSection.vue'

const isLightHeader = ref(false)
const sections = []
let observer

onMounted(() => {
  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          isLightHeader.value = entry.target.classList.contains('light-section')
        }
      })
    },
    { threshold: 0.5 },
  )

  sections.forEach((cmp) => {
    if (cmp?.$el) {
      observer.observe(cmp.$el)
    }
  })
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<style scoped></style>
