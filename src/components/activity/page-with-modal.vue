<script lang="ts" setup>
import { ref } from 'vue';
import TheLayout from '../for-tutorial/layouts/the-layout.vue';
import TheModal from './the-modal/the-modal.vue';
import BaseButton from '../for-tutorial/base-button.vue';

const refTheModal1 = ref<InstanceType<typeof TheModal>>();
const refTheModal2 = ref<InstanceType<typeof TheModal>>();

const handleClickShowModal1 = () => {
  refTheModal1.value?.showModal();
};
const handleClickShowModal2 = () => {
  refTheModal2.value?.showModal();
};
</script>

<template>
  <TheLayout>
    <TheModal ref="refTheModal1" :size="'lg'">
      <template #title>MODAL 1</template>
      <template #body-content>BODY CONTENT 1</template>
    </TheModal>

    <TheModal ref="refTheModal2" :size="'sm'">
      <template #title>MODAL 2</template>
      <template #body-content>BODY CONTENT 2</template>
    </TheModal>

    <BaseButton @click="handleClickShowModal1">
      <template #label> Show Modal 1 </template>
    </BaseButton>

    <BaseButton @click="handleClickShowModal2">
      <template #label> Show Modal 2</template>
    </BaseButton>
  </TheLayout>
</template>

<style lang="scss"></style>
