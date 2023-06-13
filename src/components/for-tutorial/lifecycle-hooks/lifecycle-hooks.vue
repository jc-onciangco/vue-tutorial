<script lang="ts" setup>
import { ref } from 'vue'
import TheLayout from '@/components/for-tutorial/layouts/the-layout.vue'
import ToastNotif from './toast-notif.vue'
import BaseButton from '../base-button.vue'

const isToastShow = ref(false)

const refToastNotif = ref<InstanceType<typeof ToastNotif>>()

const handleShowToast = () => {
  isToastShow.value = !isToastShow.value
}

const handleClickChangeMessage = () => {
  refToastNotif.value?.changeMessage('Universe')
}

const handleClickChangeStyle = () => {
  refToastNotif.value?.changeStyle({
    backgroundColor: 'blue',
    color: 'white'
  })
}
</script>

<template>
  <TheLayout>
    <div class="toast-notif-wrapper">
      <ToastNotif v-if="isToastShow" ref="refToastNotif" />
    </div>

    <div class="d-flex flex-column gap-2">
      <BaseButton @click="handleShowToast">
        <template #label> Show toast </template>
      </BaseButton>

      <BaseButton @click="handleClickChangeMessage">
        <template #label> Change Message </template>
      </BaseButton>

      <BaseButton @click="handleClickChangeStyle">
        <template #label> Change Style </template>
      </BaseButton>
    </div>
  </TheLayout>
</template>

<style lang="scss" scoped>
.toast-notif-wrapper {
  position: absolute;
  top: 1rem;
}
</style>
