<script lang="ts" setup>
import { ref } from 'vue';
import ModalBackdrop from './gallery-modal-backdrop.vue';
import ModalContent from './gallery-modal-content.vue';
import type { Idatasource } from '../explore.vue';

defineProps<{
  size?: 'sm' | 'lg' | 'full';
  dataSource?: Idatasource;
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
      :data-source="dataSource"
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