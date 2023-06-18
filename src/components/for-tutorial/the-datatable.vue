<script lang="ts" setup>
export interface IColumns {
  headerName: string;
  headerKey: string;
}

defineProps<{
  column: IColumns[];
  dataSource: Record<IColumns['headerKey'], any>[];
  id: string | number;
}>();
</script>

<template>
  <table class="table w-75 table-dark table-striped">
    <thead>
      <tr class="align-middle">
        <template v-for="col in column" :key="col.headerKey">
          <th scope="col ">
            <slot :name="`header-th-${col.headerKey}`">{{ col.headerName }}</slot>
          </th>
        </template>
      </tr>
    </thead>
    <tbody>
      <template v-for="item in dataSource" :key="item[id]">
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
</template>

<style lang="scss" scoped>
tbody {
  font-size: 0.8rem;
}
</style>
