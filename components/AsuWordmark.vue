<script setup lang="ts">
import { computed, onMounted, onUnmounted, ref } from 'vue'
import maroonSrc from '../assets/asu-wordmark-maroon.png'
import whiteSrc from '../assets/asu-wordmark-white.png'

const props = withDefaults(
  defineProps<{
    /** Force a specific variant; otherwise follows dark mode */
    variant?: 'auto' | 'maroon' | 'white'
  }>(),
  {
    variant: 'auto',
  },
)

const isDark = ref(false)
let observer: MutationObserver | null = null

onMounted(() => {
  const html = document.documentElement
  const update = () => {
    isDark.value = html.classList.contains('dark')
  }
  update()
  observer = new MutationObserver(update)
  observer.observe(html, { attributes: true, attributeFilter: ['class'] })
})

onUnmounted(() => {
  observer?.disconnect()
})

const src = computed(() => {
  if (props.variant === 'white') return whiteSrc
  if (props.variant === 'maroon') return maroonSrc
  return isDark.value ? whiteSrc : maroonSrc
})
</script>

<template>
  <img :src="src" alt="Arizona State University" class="dmml-asu-wordmark" />
</template>
