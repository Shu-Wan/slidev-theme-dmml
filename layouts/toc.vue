<script setup lang="ts">
import { useNav, useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import Footer from '../components/Footer.vue'

const { $frontmatter } = useSlideContext()
const { slides, go } = useNav()

const fm = computed(() => ($frontmatter as any) || {})

const entries = computed(() => {
  return (slides.value || [])
    .filter((s: any) => {
      const m = s?.meta?.slide?.frontmatter || s?.meta?.frontmatter || {}
      if (m.hideInToc) return false
      return m.layout === 'section'
    })
    .map((s: any, i: number) => {
      const m = s?.meta?.slide?.frontmatter || s?.meta?.frontmatter || {}
      return {
        no: s?.no ?? i + 1,
        num: m.num || m.number || String(i + 1).padStart(2, '0'),
        title: m.title || 'Section',
        subtitle: m.subtitle || '',
      }
    })
})

function jumpTo(no: number) {
  go(no)
}
</script>

<template>
  <div class="slidev-layout toc dmml-toc">
    <header class="dmml-toc__title">
      {{ fm.heading || 'Contents' }}
    </header>
    <section class="dmml-toc__body">
      <ol class="dmml-toc__list">
        <li v-for="e in entries" :key="e.no">
          <button type="button" @click="jumpTo(e.no)">
            <span class="dmml-toc__num">{{ e.num }}</span>
            <span class="dmml-toc__itemtitle">{{ e.title }}</span>
            <span v-if="e.subtitle" class="dmml-toc__itemsub">{{ e.subtitle }}</span>
          </button>
        </li>
      </ol>
    </section>
    <Footer />
  </div>
</template>
