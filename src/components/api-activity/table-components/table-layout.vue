<script lang="ts" setup generic="T">
import TablePopper from './table-popper.vue';
import dayjs from 'dayjs';

export interface IColumns {
  headerName: string;
  headerKey: string;
}

defineProps<{
  columns: IColumns[];
  dataSource: T[];
  pKey: keyof T;
}>();

const rowHeaders = [
  {
    rowHeaderName: 'Account Name'
  },
  {
    rowHeaderName: 'Account Code'
  },
  {
    rowHeaderName: 'Account Type'
  },
  {
    rowHeaderName: 'Period Covered'
  },
  {
    rowHeaderName: 'Anniversary Date'
  },
  {
    rowHeaderName: 'Billing Schedule'
  },
  {
    rowHeaderName: 'Mother Account'
  },
  {
    rowHeaderName: 'Address'
  },
  {
    rowHeaderName: 'Office No'
  },
  {
    rowHeaderName: 'Website'
  }
];

const handlePolicyDateConversion = (fromDate: Date, toDate: Date) => {
  const from = dayjs(fromDate).format('MM/DD/YYYY');
  const to = dayjs(toDate).format('MM/DD/YYYY');
  const combinedString = from + ' - ' + to;
  return combinedString;
};

const handleEncodedDateConversion = (encodedDate: Date) => {
  return dayjs(encodedDate).format('MM/DD/YYYY');
};

const handleEmptyStrings = (data: string) => {
  if (data === '') {
    return 'NOT SPECIFIED';
  } else {
    return data;
  }
};

const handleAddress = (street: string, city: string, province: string) => {
  return handleEmptyStrings(street + ' ' + city + ' ' + province);
};
</script>

<template>
  <table class="table table-light table-striped">
    <thead>
      <tr class="align-middle text-center">
        <template v-for="col in columns" :key="col.headerKey">
          <slot :name="`header-th-${col.headerKey}`">
            <th>{{ col.headerName }}</th>
          </slot>
        </template>
      </tr>
    </thead>
    <tbody>
      <template v-for="data in dataSource" :key="data[pKey]">
        <tr>
          <template v-for="col in columns" :key="col.headerKey">
            <td>
              <slot :name="`body-td-${col.headerKey}`" :rowData="data">
                {{ data[col.headerKey as keyof typeof data] }}
              </slot>
            </td>
          </template>
        </tr>
      </template>
    </tbody>
  </table>
</template>

<style scoped>
table {
  font-size: 0.8rem;
}
.icon-size {
  width: 30px;
  height: 30px;
}

.header-style {
  text-align: center;
}

.cell-size-col1 {
  width: 120px;
  text-align: left;
}

.cell-size-col2 {
  width: 90px;
}

.cell-size-col3 {
  width: 150px;
  text-align: right;
}

.footer-btn {
  padding: 10px;
  margin: 0 auto;
  max-width: 100%;
}

.view-btn {
  display: block;
  width: 100%;
  border: none;
  border-radius: 8px;
  background-image: linear-gradient(to top, #f2994a 43%, #f2c94c 100%);
  padding: 14px 28px;
  font-size: 16px;
  cursor: pointer;
  text-align: center;
  color: white;
}

.heading {
  color: #313030;
  font-size: 20px;
  margin: 0;
}

.sub-heading {
  color: gray;
  font-size: 15px;
}

.cell-style {
  vertical-align: middle;
}

.cell-style-gray {
  font-size: 15px;
  color: gray;
}
</style>
