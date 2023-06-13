<script lang="ts" setup></script>

<template>
  <div class="for-tutorial">
    <slot></slot>
  </div>
</template>

<style lang="scss">
.for-tutorial {
  width: 100%;
  height: 100vh;
  //to center the element
  display: flex;
  justify-content: center;
  align-items: center;
  //to center the element
  background-color: white;
}
</style>
