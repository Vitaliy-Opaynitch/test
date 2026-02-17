<template>
  <section
    class="forecast"
    data-observe-section
    data-header="dark"
    @mouseenter="showButton = true"
    @mouseleave="showButton = false"
    @mousemove="moveButton"
  >
    <h2 class="forecast__title">
      Still Not Sure<br />
      What Results Can You Expect?
    </h2>

    <p class="forecast__subtitle">
      Find out how many views AI Metadata Translation can bring to your channel, and how much time
      it saves!
    </p>

    <button class="forecast__button" ref="buttonRef" v-show="showButton">Get Forecast</button>

    <img src="@/assets/triangle.svg" alt="triangle" class="forecast__icon triangle" />
    <img src="@/assets/cross.svg" alt="cross" class="forecast__icon cross" />
    <img src="@/assets/circle.svg" alt="circle" class="forecast__icon circle" />
  </section>
</template>

<script setup>
import { ref } from 'vue'
import gsap from 'gsap'

const showButton = ref(false)
const buttonRef = ref(null)

function moveButton(e) {
  if (!buttonRef.value) return

  const section = e.currentTarget.getBoundingClientRect()

  const x = e.clientX - section.left
  const y = e.clientY - section.top

  gsap.to(buttonRef.value, {
    x,
    y,
    duration: 0.3,
    ease: 'power3.out',
  })
}
</script>

<style lang="scss" scoped>
.forecast {
  margin-top: 12rem;
  position: relative;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
  background: #000;
  text-align: center;
  overflow: hidden;

  &__title {
    padding-top: 5rem;
    font-size: 80px;
    line-height: 1;
    font-weight: 600;
    margin: 0 0 18px;
  }

  &__subtitle {
    margin-top: 20px;
    color: #cfcfcf;
    max-width: 720px;
    font-size: 22px;
    line-height: 1.6;
  }

  &__button {
    position: absolute;
    top: 0;
    left: 0;
    transform: translate(-50%, -50%);
    width: 175px;
    height: 175px;
    border-radius: 50%;
    background: #2e59e7;
    text-transform: uppercase;
    z-index: 20;
  }

  &__icon {
    position: absolute;
    z-index: 8;
  }

  & .triangle {
    top: 48px;
    left: 28px;
    width: 78px;
    transform: rotate(2deg);
  }

  & .cross {
    bottom: 22px;
    left: 24px;
    width: 65px;
    transform: rotate(12deg);
  }

  & .circle {
    bottom: 28px;
    right: 32px;
    width: 62px;
  }
}
</style>
