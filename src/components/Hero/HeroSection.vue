<template>
  <section
    class="relative bg-black text-white min-h-screen flex items-center justify-center px-8"
    data-observe-section
    data-header="dark"
  >
    <div class="absolute inset-0 overflow-hidden">
      <svg class="w-full h-full" xmlns="http://www.w3.org/2000/svg" preserveAspectRatio="none">
        <path
          d="M0 200 Q 200 100 400 200 T 800 200"
          stroke="#e43aff"
          stroke-width="3"
          fill="none"
        />
        <path
          d="M0 300 Q 200 400 400 300 T 800 300"
          stroke="#3aff68"
          stroke-width="3"
          fill="none"
        />
        <path
          d="M0 400 Q 200 250 400 400 T 800 400"
          stroke="#3a9aff"
          stroke-width="3"
          fill="none"
        />
      </svg>
    </div>

    <div class="relative max-w-6xl w-full">
      <div class="flex flex-col space-y-6 lg:w-2/3">
        <h2 class="text-[140px] md:text-7xl font-bold leading-tight">AI YouTube</h2>
        <div class="flex">
          <button
            class="gradient-border-button relative flex items-center px-5 py-3 text-[17px] rounded-lg text-white font-semibold bg-[#0E0E0E]/10 backdrop-blur-[8px] overflow-hidden transform transition-all duration-300 ease-out hover:scale-110"
          >
            <span class="relative z-10 flex items-center gap-2">
              <span class="uppercase font-semibold">What is this?</span>
              <HeroIcon />
            </span>
            <span class="absolute inset-0 pointer-events-none border-gradient rounded-lg"></span>
          </button>
          <h2 class="text-[140px] md:text-7xl font-bold leading-tight ml-[20px]">Metadata</h2>
        </div>

        <div class="flex">
          <h2 class="text-[140px] md:text-7xl font-bold leading-tight">Translation</h2>
          <p class="text-[17px] ml-[20px] mb-6 w-[236px]">
            Take Your YouTube Content Global by Localizing Your YouTube Metadata.
          </p>
        </div>
      </div>
      <div class="flex justify-end mt-10 lg:mt-0">
        <button
          ref="btnRef"
          class="w-[144px] h-[144px] flex items-center justify-center bg-blue-500 rounded-full text-sm font-semibold uppercase -mt-10 -mr-2"
        >
          Try for free
        </button>
      </div>
    </div>
  </section>
</template>

<script setup>
import HeroIcon from './HeroIcon.vue'
import { ref, onMounted, onBeforeUnmount } from 'vue'
import gsap from 'gsap'

const btnRef = ref(null)

const handleMouseMove = (e) => {
  const btn = btnRef.value
  if (!btn) return

  const rect = btn.getBoundingClientRect()
  const x = (e.clientX - rect.left - rect.width / 2) / 6
  const y = (e.clientY - rect.top - rect.height / 2) / 6

  gsap.to(btn, {
    duration: 0.6,
    x: x,
    y: y,
    ease: 'power3.out',
  })
}

const handleMouseLeave = () => {
  const btn = btnRef.value
  if (!btn) return

  gsap.to(btn, {
    duration: 0.5,
    x: 0,
    y: 0,
    ease: 'power3.out',
  })
}

onMounted(() => {
  const btn = btnRef.value
  btn.addEventListener('mousemove', handleMouseMove)
  btn.addEventListener('mouseleave', handleMouseLeave)
})

onBeforeUnmount(() => {
  const btn = btnRef.value
  btn.removeEventListener('mousemove', handleMouseMove)
  btn.removeEventListener('mouseleave', handleMouseLeave)
})
</script>

<style scoped>
.gradient-border-button {
  position: relative;
  border-radius: 12px;
  overflow: hidden;
}

.border-gradient {
  position: absolute;
  inset: 0;
  padding: 2px;
  border-radius: inherit;
  pointer-events: none;
  background: linear-gradient(90deg, #ffffff, #fd86ff, #fb38ff, #3858ff, #8bff78);
  background-size: 200% 100%;
  -webkit-mask:
    linear-gradient(#fff 0 0) content-box,
    linear-gradient(#fff 0 0);
  -webkit-mask-composite: xor;
  mask-composite: exclude;
  transition: background-position 0.5s ease;
}

.gradient-border-button:hover .border-gradient {
  background-position: 100% 0;
}
</style>
