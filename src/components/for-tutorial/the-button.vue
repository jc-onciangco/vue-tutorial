<script lang="ts" setup>
import { ref } from 'vue'

const username = ref('Juan')
</script>

<template>
  <button class="d-flex align-items-center">
    <slot name="left-icon">
      <i class="bi bi-123"></i>
    </slot>
    <slot name="label" :username="username"></slot>
    <slot name="right-icon"></slot>
  </button>
</template>

<style lang="scss"></style>
