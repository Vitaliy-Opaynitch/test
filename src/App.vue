<template>
  <HeaderSection :isLight="isLightHeader" />
  <HeroSection />
  <QuestionSection />
  <ForecastSection />
  <StepsSection />
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue'
import HeaderSection from './components/Header/HeaderSection.vue'
import HeroSection from './components/Hero/HeroSection.vue'
import QuestionSection from './components/QuestionSection.vue'
import ForecastSection from './components/ForecastSection.vue'
import StepsSection from './components/StepsSection.vue'

const isLightHeader = ref(false)
let observer

onMounted(async () => {
  await nextTick()
  const sectionEls = document.querySelectorAll('[data-observe-section]')
  if (!sectionEls.length) return

  observer = new IntersectionObserver(
    (entries) => {
      const intersecting = entries.filter((e) => e.isIntersecting)
      if (!intersecting.length) return
      const mostVisible = intersecting.reduce((best, e) =>
        e.intersectionRatio > best.intersectionRatio ? e : best,
      )
      isLightHeader.value = mostVisible.target.dataset.header === 'light'
    },
    { threshold: [0.25, 0.5, 0.75] },
  )

  sectionEls.forEach((el) => observer.observe(el))
})

onBeforeUnmount(() => {
  observer?.disconnect()
})
</script>
