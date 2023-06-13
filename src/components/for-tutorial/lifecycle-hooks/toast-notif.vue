<script lang="ts" setup>
import {
  reactive,
  ref,
  onMounted,
  onBeforeMount,
  onUnmounted,
  onBeforeUnmount,
  onUpdated,
  onBeforeUpdate,
  type CSSProperties
} from 'vue'

const message = ref('Hello World!')
const style = reactive<CSSProperties>({
  backgroundColor: 'yellow',
  color: 'black'
})

onMounted(() => {
  console.log('The toast was mounted')
})

onBeforeMount(() => {
  console.log('The toast is about to mount')
})

onUnmounted(() => {
  console.log('The toast was unmounted')
})

onBeforeUnmount(() => {
  console.log('The toast is about to unmount')
})

onBeforeUpdate(() => {
  console.log('The toast component is about to update')
})

onUpdated(() => {
  console.log('The toast component was updated')
})

const changeMessage = (_message: string) => {
  message.value = `Hello ${_message}`
}

const changeStyle = (_style: CSSProperties) => {
  Object.assign(style, _style)
}

defineExpose({
  changeMessage,
  changeStyle
})
</script>

<template>
  <div class="toast-notif shadow-sm rounded-3 p-2" :style="style">
    {{ message }}
  </div>
</template>

<style lang="scss">
.toast-notif {
  width: 300px;
}
</style>
