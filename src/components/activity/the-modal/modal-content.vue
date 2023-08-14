<script lang="ts" setup>
import BaseButton from '@/components/for-tutorial/base-button.vue';
</script>

<template>
  <div class="custom-modal shadow-3 rounded-3 w-75">
    <div class="d-flex flex-column h-100">
      <slot name="modal-header">
        <div
          class="w-100 p-2 px-3 d-flex align-items-center justify-content-between bg-primary rounded-top"
        >
          <div>
            <slot name="modal-title">
              <small>template here with #modal-title</small>
            </slot>
          </div>
          <div>X</div>
        </div>
      </slot>

      <div class="flex-fill">
        <slot></slot>
      </div>

      <slot name="modal-footer">
        <div
          class="w-100 p-2 px-3 d-flex align-items-center justify-content-between bg-primary bg-opacity-10 rounded-bottom"
        >
          <div></div>
          <div>
            <BaseButton> <template #label> Close </template></BaseButton>
          </div>
        </div>
      </slot>
    </div>
  </div>
</template>

<style lang="scss">
.custom-modal {
  //   min-height: 500px;
  background-color: white;
}
</style>
