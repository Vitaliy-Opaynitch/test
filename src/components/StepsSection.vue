<template>
  <section
    class="steps light-section"
    aria-label="Process steps"
    data-observe-section
    data-header="light"
    ref="sectionRef"
  >
    <div class="steps__wrapper">
      <article
        v-for="(step, index) in steps"
        :key="step.id"
        class="steps__block"
        :class="{ 'steps__block--active': activeStep === index }"
        :aria-label="`Step ${index + 1}: ${step.title}`"
        :aria-current="activeStep === index ? 'step' : undefined"
        ref="blockRefs"
      >
        <div class="steps__content">
          <span class="steps__number" aria-hidden="true">{{ index + 1 }}</span>
          <h4 class="steps__title">{{ step.title }}</h4>
          <p class="steps__desc">{{ step.description }}</p>
        </div>
        <div class="steps__image-wrapper">
          <img
            class="steps__image"
            :src="step.image"
            :alt="step.title"
            loading="lazy"
            fetchpriority="low"
          />
        </div>
      </article>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import step1 from '@/assets/step1.svg'
import step2 from '@/assets/step2.svg'
import step3 from '@/assets/step3.svg'

const sectionRef = ref(null)
const blockRefs = ref([])
const activeStep = ref(0)

const steps = [
  {
    id: 'connect-channel',
    title: 'Connect Your Channel',
    description:
      "Link your channel to AIR Media-Tech with just a few clicks. It's an ultimate space for creators with over 30 tailored services, including AI Metadata translation.",
    image: step1,
  },
  {
    id: 'get-translations',
    title: 'Get Translations',
    description:
      'AI Metadata Translation analyzes your channel, generates translations in minutes, and adds them to your channel automatically.',
    image: step2,
  },
  {
    id: 'monitor-growth',
    title: 'Monitor Growth',
    description:
      'Boost visibility and grow worldwide with AI optimization, localization, and audience engagement tools.',
    image: step3,
  },
]

let observer = null

onMounted(() => {
  const blocks = blockRefs.value
  if (!blocks.length) return

  const ratios = new Array(blocks.length).fill(0)

  observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        const index = blocks.indexOf(entry.target)
        if (index === -1) return
        ratios[index] = entry.intersectionRatio
      })
      const maxIndex = ratios.reduce((best, r, i) => (r > ratios[best] ? i : best), 0)
      if (ratios[maxIndex] > 0) {
        activeStep.value = maxIndex
      }
    },
    {
      root: null,
      rootMargin: '-10% 0px -10% 0px',
      threshold: [0, 0.1, 0.2, 0.3, 0.5, 0.7, 1],
    },
  )

  blocks.forEach((el) => observer.observe(el))
})

onUnmounted(() => {
  observer?.disconnect()
})
</script>

<style lang="scss" scoped>
.steps {
  padding: 60px 0;
  background: #fff;

  &__wrapper {
    display: flex;
    flex-direction: column;
    gap: 120px;
    max-width: 1200px;
    margin: 0 auto;
  }

  &__block {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 48px;
    min-height: 380px;
    opacity: 0.45;
    transform: scale(0.98);
    transition:
      opacity 0.5s ease,
      transform 0.5s ease;

    &--active {
      opacity: 1;
      transform: scale(1);
    }
  }

  &__content {
    flex: 0 1 42%;
    display: flex;
    flex-direction: column;
    gap: 16px;
    min-width: 0;
  }

  &__number {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    font-weight: bold;
    color: #000;
    background: #fff;
    border: 2px solid #000;
    border-radius: 50%;
  }

  &__title {
    margin: 0;
    font-size: 37px;
    font-weight: 600;
    line-height: 1.3;
    color: #000;
  }

  &__desc {
    margin: 0;
    font-size: 16px;
    line-height: 1.6;
    color: #555;
  }

  &__image-wrapper {
    flex: 1 1 60%;
    min-width: 0;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__image {
    max-width: 100%;
    width: 100%;
    max-height: 420px;
    height: auto;
    object-fit: contain;
  }
}
</style>
