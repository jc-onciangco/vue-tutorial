<script lang="ts" setup>
import { ref } from 'vue';
import ModalBackdrop from './modal-backdrop.vue';
import ModalContent from './modal-content.vue';

defineProps<{
  size?: 'sm' | 'lg' | 'full';
}>();

const isModalOpen = ref(false);

const showModal = () => (isModalOpen.value = true);
const closeModal = () => (isModalOpen.value = false);

defineExpose({
  showModal,
  closeModal
});
</script>

<template>
  <ModalBackdrop v-if="isModalOpen" @close-modal="closeModal">
    <ModalContent
      :class="{
        'w-25': size === 'sm',
        'w-50': !size,
        'w-75': size === 'lg',
        'w-100': size === 'full'
      }"
    >
      <template #modal-title>
        <slot name="title"></slot>
      </template>
      <template #default>
        <slot name="body-content"></slot>
      </template>
    </ModalContent>
  </ModalBackdrop>
</template>

<style lang="scss"></style>
