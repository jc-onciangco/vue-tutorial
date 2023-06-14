<script lang="ts" setup>
const emits = defineEmits<{
  (e: 'closeModal'): void;
}>();

const handleClickCloseModal = () => {
  emits('closeModal');
};
</script>

<template>
  <div class="custom-modal-backdrop">
    <div class="custom-modal-content-wrapper py-5">
      <div class="outside-click" @click="handleClickCloseModal"></div>
      <slot></slot>
    </div>
  </div>
</template>

<style lang="scss">
.custom-modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.6);
  backdrop-filter: blur(10px);
  z-index: 100;
  overflow-y: auto;

  .custom-modal-content-wrapper {
    position: relative;
    width: 100%;
    inset: 0;
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .outside-click {
    position: absolute;
    inset: 0;
  }
}
</style>
