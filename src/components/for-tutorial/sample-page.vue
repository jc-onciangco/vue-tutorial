<script lang="ts" setup>
import BaseButton from './base-button.vue';
import TheLayout from './layouts/the-layout.vue';
import TheDatatable from './the-datatable.vue';
import { onMounted, ref } from 'vue';

const column = [
  {
    headerName: 'Email',
    headerKey: 'email'
  },
  {
    headerName: 'Name',
    headerKey: 'name'
  },
  {
    headerName: 'Phone',
    headerKey: 'phone'
  },
  {
    headerName: 'Username',
    headerKey: 'username'
  }
];

const dataSource = ref();

onMounted(async () => {
  const res = await fetch('https://jsonplaceholder.typicode.com/users');

  const data = await res.json();

  dataSource.value = data;
  console.log(data);
});
</script>

<template>
  <TheLayout>
    <TheDatatable :column="column" :data-source="dataSource">
      <template #body-td-name="{ data }">
        {{ data.name.toUpperCase() }}
      </template>
    </TheDatatable>
    <!-- <BaseButton class="shadow-lg" id="button" :size="'lg'">
      <template #left-icon><i class="bi bi-6-square-fill"></i></template>
      <template #label> Save</template>
    </BaseButton> -->
  </TheLayout>
</template>
