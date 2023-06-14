<script lang="ts" setup>
import { computed } from 'vue';

type TColor = 'primary' | 'secondary' | 'success' | 'warning' | 'danger' | 'info';

type TSize = 'sm' | 'lg';

const props = defineProps<{
  color?: TColor;
  size?: TSize;
  outline?: boolean;
}>();

const getColor = () => {
  const color = ['btn', props.color || 'primary'];

  if (props.outline) {
    color.splice(1, 0, 'outline');
  }

  const className = color.join('-');

  return className;
};

const getSize = () => {
  if (props.size) {
    const color = ['btn', props.size];

    const className = color.join('-');

    return className;
  }
};
</script>

<script lang="ts">
export default {
  inheritAttrs: false
};
</script>

<template>
  <button type="button" class="btn d-flex gap-2" :class="[getColor(), getSize()]">
    <slot v-if="$slots['left-icon']" name="left-icon">
      <div class="left-icon">
        <i class="bi bi-download"></i>
      </div>
    </slot>

    <div class="text-center w-100" v-bind="$attrs">
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
