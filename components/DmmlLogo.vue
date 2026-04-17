<script setup lang="ts">
import logoUrl from '../assets/dmml-logo.png'
</script>

<template>
  <span
    class="dmml-logo"
    role="img"
    aria-label="DMML"
    :style="{
      maskImage: `url(${logoUrl})`,
      WebkitMaskImage: `url(${logoUrl})`,
    }"
  />
</template>

<style scoped>
.dmml-logo {
  display: inline-block;
  background-color: currentColor;
  mask-repeat: no-repeat;
  mask-position: center;
  mask-size: contain;
  -webkit-mask-repeat: no-repeat;
  -webkit-mask-position: center;
  -webkit-mask-size: contain;
}
</style>
