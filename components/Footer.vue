<script setup lang="ts">
import { useNav, useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import AsuWordmark from './AsuWordmark.vue'
import DmmlLogo from './DmmlLogo.vue'

const { currentPage, total } = useNav()
const { $slidev, $frontmatter } = useSlideContext()

const title = computed<string>(() => {
  const fm = ($frontmatter as any) || {}
  return (
    (fm.footerTitle as string) || (fm.title as string) || ($slidev?.configs?.title as string) || ''
  )
})
</script>

<template>
  <footer class="dmml-footer">
    <div class="dmml-footer__left">
      <AsuWordmark class="dmml-footer__asu" />
    </div>
    <div class="dmml-footer__title">{{ title }}</div>
    <div class="dmml-footer__right">
      <span class="dmml-footer__pagenum">{{ currentPage }} / {{ total }}</span>
      <DmmlLogo class="dmml-footer__logo" />
    </div>
  </footer>
</template>
