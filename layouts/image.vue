<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import Footer from '../components/Footer.vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})

const layoutClass = computed(() => {
  const position = fm.value.position || 'full'
  if (position === 'full') return ''
  if (position === 'right') return 'dmml-image--split reverse'
  return 'dmml-image--split'
})

const stageClass = computed(() =>
  fm.value.fill ? 'dmml-image__stage dmml-image__stage--fill' : 'dmml-image__stage',
)
</script>

<template>
  <div class="slidev-layout image dmml-image" :class="layoutClass">
    <div :class="stageClass">
      <img v-if="fm.image" :src="fm.image" :alt="fm.alt || ''" />
    </div>

    <div v-if="fm.position && fm.position !== 'full'" class="dmml-image__caption">
      <div v-if="fm.tag" class="dmml-image__tag">{{ fm.tag }}</div>
      <h1 v-if="fm.title">{{ fm.title }}</h1>
      <div><slot /></div>
    </div>
    <Footer />
  </div>
</template>
