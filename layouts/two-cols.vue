<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import Footer from '../components/Footer.vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})

const gridStyle = computed(() => {
  const split = fm.value.split || '1fr 1fr'
  return { gridTemplateColumns: split }
})
</script>

<template>
  <div class="slidev-layout two-cols dmml-two-cols">
    <header v-if="fm.heading" class="dmml-default__header">
      <h1>{{ fm.heading }}</h1>
    </header>
    <section class="dmml-two-cols__grid" :style="gridStyle">
      <div class="dmml-two-cols__left">
        <slot name="left" />
        <slot name="default" />
      </div>
      <div class="dmml-two-cols__right">
        <slot name="right" />
      </div>
    </section>
    <Footer />
  </div>
</template>
