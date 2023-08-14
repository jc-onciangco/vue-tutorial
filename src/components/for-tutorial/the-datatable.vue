<script lang="ts" setup>
export interface IColumns {
  headerName: string;
  headerKey: string;
}

defineProps<{
  column: IColumns[];
  dataSource: Record<IColumns['headerKey'], any>[];
}>();
</script>

<template>
  <table class="table w-75 table-dark table-striped">
    <thead>
      <tr>
        <template v-for="col in column" :key="col.headerKey">
          <th scope="col">{{ col.headerName }}</th>
        </template>
      </tr>
    </thead>
    <tbody>
      <template v-for="item in dataSource" :key="item.id">
        <tr>
          <template v-for="col in column" :key="col.headerKey">
            <td>
              <slot :name="`body-td-${col.headerKey}`" :data="item">{{ item[col.headerKey] }}</slot>
            </td>
          </template>
        </tr>
      </template>
    </tbody>
  </table>
  <!-- <table class="table w-75 table-dark table-striped">
    <thead>
      <tr>
        <th scope="col">#</th>
        <th scope="col">First</th>
        <th scope="col">Last</th>
        <th scope="col">Handle</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <th scope="row">1</th>
        <td>Mark</td>
        <td>Otto</td>
        <td>@mdo</td>
      </tr>
      <tr>
        <th scope="row">2</th>
        <td>Jacob</td>
        <td>Thornton</td>
        <td>@fat</td>
      </tr>
      <tr>
        <th scope="row">3</th>
        <td colspan="2">Larry the Bird</td>
        <td>@twitter</td>
      </tr>
    </tbody>
  </table> -->
</template>
