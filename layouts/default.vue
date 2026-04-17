<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import Footer from '../components/Footer.vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})
</script>

<template>
  <div class="slidev-layout default dmml-default">
    <header v-if="fm.heading" class="dmml-default__header">
      <h1>{{ fm.heading }}</h1>
    </header>
    <section class="dmml-default__body">
      <slot />
    </section>
    <Footer />
  </div>
</template>
