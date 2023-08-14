<script lang="ts" setup>
import { ref } from 'vue';
import ModalBackdrop from './modal-backdrop.vue';
import ModalContent from './modal-content.vue';

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
    <ModalContent>
      <template #modal-title> </template>
      <template #default><div style="height: 1000px"></div></template>
    </ModalContent>
  </ModalBackdrop>
</template>

<style lang="scss"></style>
