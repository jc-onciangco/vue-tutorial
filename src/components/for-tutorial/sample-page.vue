<script lang="ts" setup>
import TheLayout from './layouts/the-layout.vue';
import TheDatatable from './the-datatable.vue';
import { onMounted, ref, reactive } from 'vue';
import axios from 'axios';

const apiEndpoint = 'api/accounts/ledger';

const queryParams = reactive({
  companyname: '11/11 trading corp.-',
  pageno: 1,
  rowctr: 10
});

const column = [
  {
    headerName: 'Options',
    headerKey: 'options'
  },
  {
    headerName: 'Account Name',
    headerKey: 'companyname'
  },
  {
    headerName: 'S',
    headerKey: 'statusintial'
  },
  {
    headerName: 'Policy Period',
    headerKey: 'policyperiod'
  },
  {
    headerName: 'Address',
    headerKey: 'encodedby'
  }
];

const dataSource = ref();

onMounted(async () => {
  // const res = await fetch('https://jsonplaceholder.typicode.com/users');
  // const data = await res.json();
  const config = {
    url: apiEndpoint,
    method: 'GET',
    params: queryParams
  };

  const res = await axios(config);

  const { data, meta } = res.data;

  dataSource.value = data;
  console.log(res.data);
});
</script>

<template>
  <TheLayout>
    <div class="w-75">
      <input type="text" class="form-control mb-2" placeholder="Search for Account Name" />
      <TheDatatable :column="column" :data-source="dataSource" :id="'compcode'" class="w-100">
        <template #header-th-companyname>
          <div>
            <div>Account Name</div>
            <div>Code</div>
          </div>
        </template>
        <template #body-td-companyname="{ data }">
          <div>
            <div>{{ data.companyname }}</div>
            <div>Code</div>
          </div>
        </template>
        <template #body-td-statusintial="{ data }">
          <span class="badge bg-secondary">{{ data.statusintial }}</span>
        </template>
      </TheDatatable>
    </div>
    <!-- <BaseButton class="shadow-lg" id="button" :size="'lg'">
      <template #left-icon><i class="bi bi-6-square-fill"></i></template>
      <template #label> Save</template>
    </BaseButton> -->
  </TheLayout>
</template>

<!-- <style lang="scss" scoped>
.wrapper {
  height: 500px;
  width: 100%;
  background-color: red;
  overflow-y: auto;
}
</style> -->
