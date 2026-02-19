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
@use '@/styles/breakpoints' as bp;
@use '@/styles/colors' as c;

.steps {
  padding: 60px 0;
  background: c.$color-white;

  @include bp.md-down {
    padding: 48px 24px;
  }

  @include bp.sm-down {
    padding: 40px 20px;
  }

  @include bp.xs-down {
    padding: 32px 16px;
  }

  @include bp.xxs-down {
    padding: 24px 12px;
  }

  &__wrapper {
    display: flex;
    flex-direction: column;
    gap: 120px;
    max-width: 1200px;
    margin: 0 auto;

    @include bp.md-down {
      gap: 80px;
    }

    @include bp.sm-down {
      gap: 56px;
    }

    @include bp.xs-down {
      gap: 40px;
    }

    @include bp.xxs-down {
      gap: 32px;
    }
  }

  &__block {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 48px;
    opacity: 0.45;
    transform: scale(0.98);
    transition:
      opacity 0.5s ease,
      transform 0.5s ease;

    @include bp.md-down {
      gap: 32px;
    }

    @include bp.sm-down {
      flex-direction: column;
      gap: 24px;
      text-align: center;
    }

    @include bp.xs-down {
      gap: 20px;
    }

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
    padding-left: 0;

    @include bp.md-down {
      padding-left: 24px;
    }

    @include bp.sm-down {
      flex: 1 1 auto;
      width: 100%;
      align-items: center;
      padding-left: 0;
    }

    @include bp.xs-down {
      gap: 12px;
    }
  }

  &__number {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    font-weight: bold;
    color: c.$color-black;
    background: c.$color-white;
    border: 2px solid c.$color-black;
    border-radius: 50%;

    @include bp.xs-down {
      width: 32px;
      height: 32px;
      font-size: 14px;
    }

    @include bp.xxs-down {
      width: 28px;
      height: 28px;
      font-size: 12px;
    }
  }

  &__title {
    margin: 0;
    font-size: 37px;
    font-weight: 600;
    line-height: 1.3;
    color: c.$color-black;

    @include bp.md-down {
      font-size: 30px;
    }

    @include bp.sm-down {
      font-size: 26px;
    }

    @include bp.xs-down {
      font-size: 22px;
    }

    @include bp.xxs-down {
      font-size: 18px;
    }
  }

  &__desc {
    margin: 0;
    font-size: 16px;
    line-height: 1.6;
    color: c.$color-text-muted;

    @include bp.md-down {
      font-size: 15px;
    }

    @include bp.xs-down {
      font-size: 14px;
    }

    @include bp.xxs-down {
      font-size: 13px;
    }
  }

  &__image-wrapper {
    flex: 1 1 60%;
    min-width: 0;
    max-width: 60%;
    display: flex;
    align-items: center;
    justify-content: center;

    @include bp.md-down {
      flex: 1 1 50%;
      max-width: 50%;
    }

    @include bp.sm-down {
      flex: 1 1 auto;
      width: 100%;
      max-width: 360px;
      margin: 0 auto;
      order: -1;
    }

    @include bp.xs-down {
      max-width: 300px;
    }

    @include bp.xxs-down {
      max-width: 260px;
    }
  }

  &__image {
    max-width: 100%;
    width: 100%;
    max-height: 420px;
    height: auto;
    object-fit: contain;

    @include bp.md-down {
      max-height: 340px;
    }

    @include bp.sm-down {
      max-height: 280px;
    }

    @include bp.xs-down {
      max-height: 220px;
    }

    @include bp.xxs-down {
      max-height: 180px;
    }
  }
}
</style>
