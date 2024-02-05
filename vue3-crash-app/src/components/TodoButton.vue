<script setup lang="ts">
import { onMounted, ref } from 'vue'
// import { useFocus } from '@vueuse/core'

const btn = ref(null)

const focusBtn = () => {
  if (btn.value) {
    btn.value.focus();
  }
};

onMounted(focusBtn);
// const { focused } = useFocus(btn, { initialValue: true })
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