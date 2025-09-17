<template>
  <section class="survey-question">
    <div class="survey-question__header-image"></div>
    <div class="survey-question__main-image"></div>

    <h2 class="survey-question__title">
      Are your videos <br />
      understandable without <br />
      voice narration?
    </h2>
    <div>
      <p class="survey-question__subtitle-text">{{ subtitle }}</p>
      <div class="survey-question__subtitle-icon"></div>
    </div>
    <div class="survey-question__answers">
      <div
        v-for="option in options"
        :key="option.value"
        class="survey-question__answer"
        :class="option.icon"
      >
        <p class="survey-question__answer-text">{{ option.label }}</p>
        <div class="survey-question__tooltip">
          <p class="survey-question__tooltip-text">{{ buttonDescription }}</p>
          <button class="survey-question__tooltip-btn" @click="handleAnswerClick(option.value)">
            <span class="survey-question__tooltip-btn-label">Start for Free</span>
          </button>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { computed } from 'vue'

const subtitle = computed(() => 'Choose answer')

const options = computed(() => [
  { label: 'Partially', value: 'partially', icon: 'icon-partially' },
  { label: 'Yes', value: 'yes', icon: 'icon-yes' },
  { label: 'No', value: 'no', icon: 'icon-no' },
])

const buttonDescription = computed(
  () =>
    "Awesome! Localizing your YouTube metadata is a perfect choice for you. Let's translate your video titles, descriptions, and tags, so people from all around the globe can discover your content.",
)

function handleAnswerClick(value) {
  console.log(value)
}
</script>

<style lang="scss" scoped>
.survey-question {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;

  &__header-image {
    height: 140px;
    width: 100%;
    background-image: url('@/assets/question_section_background_image.svg');
    background-repeat: no-repeat;
    background-position: top center;
  }

  &__main-image {
    margin-top: 50px;
    width: 200px;
    height: 200px;
    background-image: url('@/assets/bullhorn_image.svg');
    background-repeat: no-repeat;
    background-position: center;
  }

  &__title {
    margin-top: 25px;
    font-size: 4.625rem;
    font-weight: 600;
  }

  &__subtitle-text {
    font-size: 2.375rem;
  }

  &__subtitle-icon {
    margin: 25px auto 0 auto;
    width: 30px;
    height: 52px;
    background-image: url('@/assets/arrow_bottom_icon_blue.svg');
    background-repeat: no-repeat;
    background-position: center;
  }

  &__answers {
    margin-top: 50px;
    display: flex;
    gap: 30px;
    font-size: 2.375rem;
    justify-content: center;
  }

  &__answer {
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #fff;
    font-weight: 500;
    background-repeat: no-repeat;
    background-position: center;
    width: 320px;
    height: 320px;
    cursor: pointer;
    transition: transform 0.3s ease;

    &:hover {
      .survey-question__tooltip {
        opacity: 1;
        visibility: visible;
        transform: translate(-50%, 0);
      }
    }
  }

  &__answer-text {
    position: absolute;
    transform: translateY(-50%);
    top: 50%;
    z-index: 10;
  }

  &__tooltip {
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, 0);
    width: 100%;
    background: #000;
    color: #fff;
    padding: 16px;
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
    z-index: 9;
  }

  &__tooltip-text {
    font-size: 14px;
    margin: 20px 0;
  }

  &__tooltip-btn {
    position: relative;
    overflow: hidden;
    width: 100%;
    max-width: 276px;
    height: 70px;
    padding: 10px 16px;
    font-size: 1.125rem;
    font-weight: 600;
    letter-spacing: 0.04em;
    border-radius: 10px;
    background-color: #0b42ff;
    color: #fff;

    &::before {
      content: '';
      position: absolute;
      inset: 0;
      background: #fff;
      border-radius: inherit;
      transform: scaleX(0);
      transform-origin: left center;
      z-index: 1;
      transition: transform 0.6s cubic-bezier(0.22, 0.9, 0.3, 1);
    }

    &:hover::before {
      transform: scaleX(1);
    }

    &-label {
      position: relative;
      z-index: 2;
      transition: color 0.3s ease;
    }

    &:hover .survey-question__tooltip-btn-label {
      color: #000;
    }
  }

  & .icon-partially {
    background-image: url('@/assets/answer_partially_icon.svg');
  }

  & .icon-yes {
    background-image: url('@/assets/answer_yes_icon.svg');
  }

  & .icon-no {
    background-image: url('@/assets/answer_no_icon.svg');
  }
}
</style>
