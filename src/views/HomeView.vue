<script setup lang="ts">
import { ref } from 'vue';
import LifecycleHooks from '@/components/for-tutorial/lifecycle-hooks/lifecycle-hooks.vue';
import PropsAndEmits from '@/components/for-tutorial/props-and-emits/props-and-emits.vue';
import TheBasic from '@/components/for-tutorial/the-basic.vue';
import BaseButton from '@/components/for-tutorial/base-button.vue';
import PageWithModal from '@/components/activity/page-with-modal.vue';
import SampleSlot from '@/components/for-tutorial/sample-slot.vue';
</script>

<template>
  <TheModal />
  <!-- <TheBasic /> -->
  <!-- <LifecycleHooks /> -->
  <!-- <PropsAndEmits /> -->
  <PageWithModal />
  <!-- <SampleSlot /> -->
</template>

<style lang="scss"></style>
