<script lang="ts" setup>
defineProps<{
  modelValue: any;
}>();

const emit = defineEmits<{
  (e: 'update:modelValue', value: any): void;
}>();

const handleInput = (e: Event) => {
  const value = (e.target as HTMLInputElement).value;
  emit('update:modelValue', value);
};
</script>

<template>
  <input
    type="text"
    class="form-control"
    placeholder="Search Company Name"
    aria-label="Username"
    aria-describedby="addon-wrapping"
    :value="modelValue"
    @input="handleInput"
  />
</template>
