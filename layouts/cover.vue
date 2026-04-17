<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'
import AsuWordmark from '../components/AsuWordmark.vue'
import DmmlLogo from '../components/DmmlLogo.vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})
</script>

<template>
  <div class="slidev-layout cover dmml-cover">
    <div class="dmml-cover__top">
      <DmmlLogo class="dmml-logo" />
    </div>

    <div class="dmml-cover__center">
      <div v-if="fm.eyebrow" class="dmml-cover__eyebrow">{{ fm.eyebrow }}</div>
      <h1 class="dmml-cover__title">
        <slot><span class="highlight">{{ fm.title }}</span></slot>
      </h1>
      <div class="dmml-cover__rule" />
      <p v-if="fm.subtitle" class="dmml-cover__subtitle">{{ fm.subtitle }}</p>
      <div v-if="fm.presenter || fm.affiliation" class="dmml-cover__meta">
        <div v-if="fm.presenter"><span class="label">Presented by</span>{{ fm.presenter }}</div>
        <div v-if="fm.affiliation"><span class="label">Affiliation</span>{{ fm.affiliation }}</div>
      </div>
    </div>

    <div class="dmml-cover__bottom">
      <AsuWordmark />
      <div v-if="fm.date" class="dmml-cover__date">{{ fm.date }}</div>
    </div>
  </div>
</template>
