<script lang="ts" setup>
import { computed } from 'vue'

type TColor = 'primary' | 'secondary' | 'success' | 'warning' | 'danger' | 'info'

const props = defineProps<{
  color?: TColor
}>()

const colors: Record<TColor, string> = {
  primary: 'btn-primary',
  secondary: 'btn-secondary',
  success: 'btn-success',
  warning: 'btn-warning',
  danger: 'btn-danger',
  info: 'btn-info'
}

const getColor = computed(() => {
  if (props.color) {
    return colors[props.color]
  }

  return 'btn-primary'
})
</script>

<template>
  <button type="button" class="btn d-flex gap-2" :class="[getColor]">
    <slot v-if="$slots['left-icon']" name="left-icon">
      <div class="left-icon">
        <i class="bi bi-download"></i>
      </div>
    </slot>
    <div class="text-center w-100">
      <slot name="label"> Label </slot>
    </div>
    <slot v-if="$slots['right-icon']" name="right-icon">
      <div class="right-icon">
        <i class="bi bi-download"></i>
      </div>
    </slot>
  </button>
</template>

<style lang="scss"></style>
