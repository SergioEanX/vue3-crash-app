<script setup lang="ts">
import { ref } from 'vue'
import { useFocus } from '@vueuse/core'

const btn = ref()
const { focused } = useFocus(btn, { initialValue: true })
</script>

<template>
<button ref="btn">
  <slot>
Create
  </slot>
</button>
</template>

<style scoped lang="scss">
button {
  padding: 8px 16px;
  border: none;
}
</style>