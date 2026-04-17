<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import DmmlLogo from '../components/DmmlLogo.vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})
</script>

<template>
  <div class="slidev-layout end dmml-end">
    <div class="dmml-end__bg" />
    <DmmlLogo class="dmml-end__logo" />
    <div class="dmml-end__main">
      <h1 class="dmml-end__thanks">{{ fm.thanks || 'Thank you' }}</h1>
      <p v-if="fm.subtitle" class="dmml-end__subtitle">{{ fm.subtitle }}</p>

      <div v-if="fm.email || fm.website || fm.github || fm.contact" class="dmml-end__contact">
        <div v-if="fm.email"><span class="k">email</span>{{ fm.email }}</div>
        <div v-if="fm.website"><span class="k">web&nbsp;&nbsp;</span>{{ fm.website }}</div>
        <div v-if="fm.github"><span class="k">gh&nbsp;&nbsp;&nbsp;</span>{{ fm.github }}</div>
        <div v-if="fm.contact"><span class="k">tel&nbsp;&nbsp;</span>{{ fm.contact }}</div>
      </div>

      <div style="margin-top: 1rem"><slot /></div>
    </div>

    <div class="dmml-end__footer">
      <span>Arizona State University · Data Mining &amp; Machine Learning Lab</span>
      <span v-if="fm.date">{{ fm.date }}</span>
    </div>
  </div>
</template>
