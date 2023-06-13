<script lang="ts" setup>
import { ref } from 'vue'
import TheLayout from '../for-tutorial/layouts/the-layout.vue'
import TheModal from './the-modal/the-modal.vue'
import BaseButton from '../for-tutorial/base-button.vue'

const refTheModal = ref<InstanceType<typeof TheModal>>()

const handleClickShowModal = () => {
  refTheModal.value?.showModal()
}
</script>

<template>
  <TheLayout>
    <TheModal ref="refTheModal" />
    <BaseButton @click="handleClickShowModal">
      <template #label> Show Modal </template>
    </BaseButton>
  </TheLayout>
</template>

<style lang="scss"></style>
