<template>
  <section class="steps" ref="stepsSection">
    <div class="steps__wrapper">
      <div class="steps__left">
        <div class="steps__line">
          <div class="steps__line-indicator" ref="lineIndicator"></div>
        </div>

        <div
          v-for="(step, index) in steps"
          :key="index"
          class="steps__item"
          :class="{
            active: activeStep === index,
            next: activeStep + 1 === index,
          }"
          ref="stepItems"
        >
          <div class="steps__number">{{ index + 1 }}</div>
          <h2 class="steps__title">{{ step.title }}</h2>
          <p class="steps__desc">{{ step.description }}</p>
        </div>
      </div>

      <div class="steps__right">
        <div class="steps__image-wrapper">
          <transition name="fade" mode="out-in">
            <img
              :key="activeStep"
              class="steps__image"
              :src="steps[activeStep].image"
              :alt="steps[activeStep].title"
            />
          </transition>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref, onMounted, onUnmounted, nextTick } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
gsap.registerPlugin(ScrollTrigger)

import step1 from '@/assets/step1.svg'
import step2 from '@/assets/step2.svg'
import step3 from '@/assets/step3.svg'

const stepsSection = ref(null)
const stepItems = ref([])
const lineIndicator = ref(null)
const activeStep = ref(0)

const steps = [
  {
    title: 'Connect Your Channel',
    description:
      'Link your channel to AIR Media-Tech with just a few clicks. It’s an ultimate space for creators with over 30 tailored services, including AI Metadata translation.',
    image: step1,
  },
  {
    title: 'Get Translations',
    description:
      'AI Metadata Translation analyzes your channel, generates translations in minutes, and adds them to your channel automatically.',
    image: step2,
  },
  {
    title: 'Monitor Growth',
    description:
      'Boost visibility and grow worldwide with AI optimization, localization, and audience engagement tools.',
    image: step3,
  },
]

let resizeHandler = null
let createdTriggers = []

onMounted(async () => {
  await nextTick()
  const indicator = lineIndicator.value
  const sectionEl = stepsSection.value
  const lineEl = sectionEl.querySelector('.steps__line')
  const items =
    stepItems.value && stepItems.value.length
      ? stepItems.value
      : Array.from(sectionEl.querySelectorAll('.steps__item'))

  if (!indicator || !lineEl || items.length === 0) return

  const computeAndBind = () => {
    createdTriggers.forEach((t) => t.kill && t.kill())
    createdTriggers = []

    const lineRect = lineEl.getBoundingClientRect()
    const lineHeight = lineRect.height
    const indicatorHeightPercent = 50
    const indicatorHeightPx = lineHeight * (indicatorHeightPercent / 100)
    const indicatorHalf = indicatorHeightPx / 2

    items.forEach((el, i) => {
      const numberEl = el.querySelector('.steps__number')
      if (!numberEl) return

      const numRect = numberEl.getBoundingClientRect()
      const centerY = numRect.top - lineRect.top + numRect.height / 2
      const topPx = centerY - indicatorHalf
      let topPercent = (topPx / lineHeight) * 100
      topPercent = Math.max(0, Math.min(100 - indicatorHeightPercent, topPercent))

      const trig = ScrollTrigger.create({
        trigger: el,
        start: 'top center',
        end: 'bottom center',
        onEnter: () => {
          activeStep.value = i
          gsap.to(indicator, { top: `${topPercent}%`, duration: 0.35, ease: 'power2.out' })
        },
        onEnterBack: () => {
          activeStep.value = i
          gsap.to(indicator, { top: `${topPercent}%`, duration: 0.35, ease: 'power2.out' })
        },
      })
      createdTriggers.push(trig)
    })
  }

  computeAndBind()
  resizeHandler = () => requestAnimationFrame(computeAndBind)
  window.addEventListener('resize', resizeHandler)
})

onUnmounted(() => {
  window.removeEventListener('resize', resizeHandler)
  createdTriggers.forEach((t) => t.kill && t.kill())
  createdTriggers = []
})
</script>

<style lang="scss" scoped>
.steps {
  padding: 120px 0;
  background: #fff;

  &__wrapper {
    display: flex;
    max-width: 1200px;
    margin: 0 auto;
    gap: 80px;
  }

  &__left {
    flex: 1;
    position: relative;
    padding-left: 60px;
  }

  &__line {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 18px;
    width: 4px;
    background: #e5e7eb;

    &-indicator {
      position: absolute;
      left: 0;
      top: 0;
      width: 4px;
      height: 20%;
      background: #2563eb;
      border-radius: 2px;
      will-change: top;
    }
  }

  &__item {
    margin-bottom: 100px;
    position: relative;
    transition:
      opacity 0.3s ease,
      color 0.3s ease;

    &.active {
      opacity: 1;
      .steps__title {
        color: #000;
      }
      .steps__desc {
        color: #333;
      }
    }

    &.next {
      opacity: 0.5;
      .steps__title,
      .steps__desc {
        color: #aaa;
      }
    }
  }

  &__number {
    width: 36px;
    height: 36px;
    border: 2px solid #000;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 16px;
    font-weight: bold;
    background: #fff;
    color: #000;
  }

  &__title {
    margin-bottom: 12px;
    font-size: 56px;
    font-weight: 600;
    line-height: 1.3;
  }

  &__desc {
    font-size: 16px;
    color: #555;
    line-height: 1.6;
  }

  &__right {
    position: relative;
    flex: 1;
    display: flex;
    align-items: flex-start;
    justify-content: center;
  }

  &__image-wrapper {
    position: sticky;
    top: 0;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  &__image {
    max-width: 100%;
    max-height: 100%;
    object-fit: contain;
    transition: opacity 0.4s ease;
    z-index: 1;
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
