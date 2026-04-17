<script setup lang="ts">
import { useSlideContext } from '@slidev/client'
import { computed } from 'vue'

const { $frontmatter } = useSlideContext()
const fm = computed(() => ($frontmatter as any) || {})
</script>

<template>
  <div class="slidev-layout section dmml-section">
    <div class="dmml-section__bg" />
    <div>
      <div v-if="fm.num || fm.number" class="dmml-section__num">
        {{ fm.num || fm.number }}
      </div>
      <h1 class="dmml-section__title">
        <slot>{{ fm.title }}</slot>
      </h1>
      <div class="dmml-section__rule" />
      <p v-if="fm.subtitle" class="dmml-section__subtitle">{{ fm.subtitle }}</p>
    </div>
    <div class="dmml-section__footer">
      <span>ASU · DMML Lab</span>
      <span v-if="fm.part">{{ fm.part }}</span>
    </div>
  </div>
</template>
