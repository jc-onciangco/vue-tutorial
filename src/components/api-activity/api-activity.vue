<script lang="ts" setup>
import ApiActivityLayout from './layout/api-activity-layout.vue';
import TableLayout, { type IColumns } from './table-components/table-layout.vue';
import { onMounted, ref, reactive, watch } from 'vue';
import axios from 'axios';
import { watchDebounced } from '@vueuse/core';
import TheLayout from '../for-tutorial/layouts/the-layout.vue';
import dayjs from 'dayjs';
import PopperAccountProfile from './popper-account-profile.vue';
import { useDebounceFn } from '@vueuse/core';
import InputText from './input-text.vue';
import InputSelectDropdown from './input-select-dropdown.vue';

export interface Iledgerdata {
  compcode: number;
  contractno: string;
  companyname: string;
  statusname: string;
  statusintial: string;
  dateenrolled: Date;
  effectivity: Date;
  expiry: Date;
  coveredfrom: Date;
  coveredto: Date;
  dateencoded: Date;
  streetaddress: string;
  cityname: string;
  provincename: string;
  encodedbyname: string;
  initial: string;
  telephone: string;
  website: string;
  billingschedule: number;
  billingscheduleinitial: string;
  billingschedulename: string;
  billingsetup: string;
  billingcompany: string;
  mothercontractno: string;
  motheraccount: string;
  accounttypedesc: string;
}

const companyNameInput = ref('');
const dataSource = ref<Iledgerdata[]>([]);
const currentPage = ref(1);
const isPrevDisabled = ref(true);
const isNextDisabled = ref(false);
const isLoading = ref(false);

const queryParams = reactive({
  contractno: 1,
  companyName: '',
  statuscode: '',
  pageNo: currentPage,
  rowCtr: 10
});

const column: IColumns[] = [
  {
    headerName: 'Corporate Profile Details',
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
    headerKey: 'address'
  },
  {
    headerName: 'Date Encoded',
    headerKey: 'dateencoded'
  }
];
// for v-model search add -> debounce
// watch(
//   () => companyNameInput.value,
//   (newValue, oldValue) => {
//     handleFetchApi();
//   }
// );

const handleEnterKeySearch = () => {
  handleFetchApi();
};

const handleFetchApi = async () => {
  const apiEndpoint = 'api/accounts/ledger';

  const config = {
    url: apiEndpoint,
    method: 'GET',
    params: queryParams
  };

  isLoading.value = true;

  const res = await axios(config);
  const { data } = res.data;

  console.log(data);

  dataSource.value = data;
};

const handleClickNext = () => {
  currentPage.value += 1;
  isPrevDisabled.value = false;
  isNextDisabled.value = true;

  handleFetchApi();
};

const handleClickPrev = () => {
  currentPage.value -= 1;
  isPrevDisabled.value = true;
  isNextDisabled.value = false;

  handleFetchApi();
};

onMounted(async () => {
  handleFetchApi();
});

const handlePolicyDateConversion = (fromDate: Date, toDate: Date) => {
  const from = dayjs(fromDate).format('MM/DD/YYYY');
  const to = dayjs(toDate).format('MM/DD/YYYY');
  const combinedString = from + ' - ' + to;
  return combinedString;
};

const handleEncodedDateConversion = (encodedDate: Date) => {
  return dayjs(encodedDate).format('MM/DD/YYYY');
};

watchDebounced(
  dataSource,
  () => {
    isLoading.value = false;
  },
  { debounce: 1000, maxWait: 3000 }
);

const debouncedFn = useDebounceFn(() => {
  handleFetchApi();
}, 1000);

const fetchDebounceApi = () => {
  debouncedFn();
};

watch(
  () => queryParams.companyName,
  (newValue) => {
    fetchDebounceApi();
  }
);
</script>

<template>
  <ApiActivityLayout>
    <!-- v-model search -->
    <!-- <div class="input-group flex-nowrap">
            <span class="input-group-text" id="addon-wrapping">🔍︎</span>
            <input type="text" class="form-control" placeholder="Search Company Name" aria-label="Username" aria-describedby="addon-wrapping" v-model="companyNameInput">
        </div> -->

    <div class="input-group flex-nowrap">
      <span class="input-group-text" id="addon-wrapping">🔍︎</span>
      {{ companyNameInput }}
      <InputText v-model="queryParams.companyName" />
      <InputSelectDropdown v-model="queryParams.statuscode" />
      <!-- <input
        type="text"
        class="form-control"
        placeholder="Search Company Name"
        aria-label="Username"
        aria-describedby="addon-wrapping"
        v-model="companyNameInput"
        @keyup.enter="handleEnterKeySearch()"
        @input="handleInput"
      /> -->
    </div>
    <div v-if="isLoading">
      <TheLayout>
        <div class="spinner-border" role="status">
          <span class="visually-hidden">Loading...</span>
        </div>
      </TheLayout>
    </div>
    <div v-else class="table-area">
      <TableLayout :data-source="dataSource" :columns="column" :p-key="'compcode'">
        <template #body-td-options="{ rowData }">
          <PopperAccountProfile :row-data="rowData" />
        </template>
        <template #header-th-companyname>
          <div>
            <div>Account Name</div>
            <div>Code</div>
          </div>
        </template>
        <template #body-td-companyname="{ rowData }">
          <div>
            <div class="fw-semibold">{{ rowData.companyname }}</div>
            <div>{{ rowData.contractno }}</div>
          </div>
        </template>
        <template #header-th-dateencoded>
          <div>
            <div>Encoded By</div>
            <div>Date Encoded</div>
          </div>
        </template>

        <template #body-td-dateencoded="{ rowData }">
          <div>
            <div class="fw-semibold">{{ rowData.encodedbyname }}</div>
            <div>{{ rowData.dateencoded }}</div>
          </div>
        </template>

        <template #body-td-address="{ rowData }">
          <div class="text-uppercase">
            {{ `${rowData.streetaddress} ${rowData.cityname} ${rowData.provincename}` }}
          </div>
        </template>
        <template #body-td-policyperiod="{ rowData }">
          <div class="text-uppercase">
            {{ handlePolicyDateConversion(rowData.effectivity, rowData.expiry) }}
          </div>
        </template>
        <template #body-td-statusintial="{ rowData }">
          <h5>
            <span class="badge bg-secondary">{{ rowData.statusintial }}</span>
          </h5>
        </template>
        <!-- <template #table-col-header>
          <th scope="col" class="header-alignment" style="width: 10px">
            <p class="heading">{{ column[0].headerName }}</p>
            <p />
          </th>
          <th scope="col" class="header-alignment" style="width: 600px">
            <p class="heading">{{ column[1].headerName }}</p>
            <p class="sub-heading">{{ column[2].headerName }}</p>
          </th>
          <th scope="col" style="width: 100px">
            <p class="heading" style="margin-left: 5px">{{ column[3].headerName }}</p>
            <p />
          </th>
          <th scope="col" class="header-alignment" style="width: 200px">
            <p class="heading">{{ column[4].headerName }}</p>
            <p />
          </th>
          <th scope="col" class="header-alignment" style="width: 400px">
            <p class="heading">{{ column[5].headerName }}</p>
            <p />
          </th>
          <th scope="col" class="header-alignment">
            <p class="heading">{{ column[6].headerName }}</p>
            <p class="sub-heading">{{ column[7].headerName }}</p>
          </th>
        </template> -->
      </TableLayout>
      <div class="pagination">
        <nav aria-label="...">
          <ul class="pagination">
            <li class="page-item" :class="isPrevDisabled ? 'disabled' : 'active'">
              <a class="page-link" @click="handleClickPrev">previous</a>
            </li>
            <li class="page-item" :class="isNextDisabled ? 'disabled' : 'active'">
              <a class="page-link" @click="handleClickNext">Next</a>
            </li>
          </ul>
        </nav>
      </div>
    </div>
    <!-- <div class="pagination">
                <div class="pagination-button" :class="isPrevDisabled ? 'disabled-button' : 'active-button'" @click="handleClickPrev"> {{ "< Prev" }} </div>
                <div class="pagination-button" :class="isNextDisabled ? 'disabled-button' : 'active-button'" @click="handleClickNext"> {{ "Next >" }}</div>
        </div> -->
  </ApiActivityLayout>
</template>

<style lang="scss" scoped>
.table-area {
  margin-top: 10px;
}

.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
}

.pagination-button {
  float: left;
  width: 10%;
}

.active-button {
  color: blue;
  cursor: pointer;
}

.disabled-button {
  color: gray;
  pointer-events: none;
}

.header-alignment {
  text-align: center;
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
</style>
