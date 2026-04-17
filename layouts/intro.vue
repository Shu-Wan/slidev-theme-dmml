<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import Footer from '../components/Footer.vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})
</script>

<template>
  <div class="slidev-layout intro dmml-intro">
    <div v-if="fm.avatar" class="dmml-intro__avatar">
      <img :src="fm.avatar" :alt="fm.name || 'Presenter'" />
    </div>
    <div>
      <h1 class="dmml-intro__name">{{ fm.name || fm.title }}</h1>
      <div v-if="fm.role" class="dmml-intro__title">{{ fm.role }}</div>
      <div v-if="fm.affiliation" class="dmml-intro__affiliation">{{ fm.affiliation }}</div>
      <div v-if="$slots.default" class="dmml-intro__bio"><slot /></div>
      <div v-if="fm.links && fm.links.length" class="dmml-intro__links">
        <a
          v-for="link in fm.links"
          :key="link.url"
          :href="link.url"
          target="_blank"
          rel="noopener"
          >{{ link.label || link.url }}</a
        >
      </div>
    </div>
    <Footer />
  </div>
</template>
