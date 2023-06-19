<script lang="ts" setup>
import type { Iledgerdata } from './api-activity.vue';

defineProps<{
  rowData: Iledgerdata;
}>();
</script>

<template>
  <button type="button" class="btn btn-primary btn-sm">
    <i class="bi bi-person-square"></i>
  </button>
</template>
