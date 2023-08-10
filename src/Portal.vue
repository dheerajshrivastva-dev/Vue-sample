<!-- Portal.vue -->
<template>
  <teleport to="#portal">
      <slot></slot>
    </teleport>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: "Vue-Portal"
});
</script>

<style scoped>
</style>
