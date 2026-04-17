<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import Footer from '../components/Footer.vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})
</script>

<template>
  <div class="slidev-layout quote dmml-quote">
    <div>
      <div class="dmml-quote__mark">“</div>
      <div class="dmml-quote__body">
        <slot>{{ fm.quote }}</slot>
      </div>
      <div v-if="fm.author || fm.source" class="dmml-quote__attribution">
        <span v-if="fm.author" class="name">{{ fm.author }}</span>
        <template v-if="fm.author && fm.source"> — </template>
        <span v-if="fm.source">{{ fm.source }}</span>
      </div>
    </div>
    <Footer />
  </div>
</template>
