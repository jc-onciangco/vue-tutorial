<script lang="ts" setup>
import ApiActivityLayout from './layout/api-activity-layout.vue'
import TableLayout from './table-components/table-layout.vue'
import { onMounted, ref, reactive, watch } from 'vue';
import axios from 'axios';
import { watchDebounced } from '@vueuse/core';
import TheLayout from '../for-tutorial/layouts/the-layout.vue';

export interface Iledgerdata {
    compcode: number,
    contractno: string,
    companyname: string,
    statusname: string,
    statusintial: string,
    dateenrolled: Date,
    effectivity: Date,
    expiry: Date,
    coveredfrom: Date,
    coveredto: Date,
    dateencoded: Date,
    streetaddress: string,
    cityname: string,
    provincename: string,
    encodedbyname: string,
    initial: string,
    telephone: string,
    website: string,
    billingschedule: number,
    billingscheduleinitial: string,
    billingschedulename: string,
    billingsetup: string,
    billingcompany: string,
    mothercontractno: string,
    motheraccount: string,
    accounttypedesc: string
}

const apiEndpoint = 'api/accounts/ledger';
const companyNameInput = ref('');
const dataSource = ref<Iledgerdata>();
const currentPage = ref(1);
const isPrevDisabled = ref(true);
const isNextDisabled = ref(false);
const isLoading = ref(false);

const queryParams = reactive({
    contractno: 1,
    companyName: companyNameInput,
    pageNo: currentPage,
    rowCtr: 10
})

const column = [
    {
        headerName: 'Corporate Profile Details',
        headerKey: 'compcode'
    },
    {
        headerName: 'Account Name',
        headerKey: 'companyname'
    },
    {
        headerName: 'Code',
        headerKey: 'contractno'
    },
    {
        headerName: 'S',
        headerKey: 'statusiinitial'
    },
    {
        headerName: 'Policy Period',
        headerKey: 'policyperiod'
    },
    {
        headerName: 'Address',
        headerKey: 'encodedby'
    },
    {
        headerName: 'Encoded By',
        headerKey: 'encodedbyname'
    },
    {
        headerName: 'Date Encoded',
        headerKey: 'dateencoded'
    }
]
// for v-model search add -> debounce
// watch(
//   () => companyNameInput.value,
//   (newValue, oldValue) => {
//     handleFetchApi();
//   }
// );

const handleEnterKeySearch = () => {
    handleFetchApi();
}

const handleFetchApi = async () => {
    const config = {
        url: apiEndpoint,
        method: 'GET',
        params: queryParams
    };
    isLoading.value = true;
    const res = await axios(config);

    const { data, meta } = res.data;

    dataSource.value = data;
}

const handleClickNext = () => {
    currentPage.value += 1;
    isPrevDisabled.value = false;
    isNextDisabled.value = true;

    handleFetchApi();
}

const handleClickPrev = () => {
    currentPage.value -= 1;
    isPrevDisabled.value = true;
    isNextDisabled.value = false;

    handleFetchApi();
}

onMounted(async () => {
    handleFetchApi();
});

watchDebounced(
    dataSource,
    () => { isLoading.value = false; },
    { debounce: 1000, maxWait: 3000}
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
            <input type="text"
                class="form-control"
                placeholder="Search Company Name"
                aria-label="Username"
                aria-describedby="addon-wrapping"
                v-model="companyNameInput"
                @keyup.enter="handleEnterKeySearch()">
        </div>
        <div v-if="isLoading">
            <TheLayout>
                <div class="spinner-border" role="status">
                    <span class="visually-hidden">Loading...</span>
                </div>
            </TheLayout>
        </div>
        <div v-else class="table-area">
            <TableLayout :data-source="dataSource">
                <template #table-col-header>
                    <th scope="col" class="header-alignment" style="width: 10px;"><p class="heading">{{ column[0].headerName }}</p><p /> </th>
                    <th scope="col" class="header-alignment" style="width: 600px;"> 
                        <p class="heading">{{ column[1].headerName }}</p>
                        <p class="sub-heading">{{ column[2].headerName }}</p>
                    </th>
                    <th scope="col" style="width: 100px;"><p class="heading" style="margin-left: 5px;">{{ column[3].headerName }}</p><p /> </th>
                    <th scope="col" class="header-alignment" style="width: 200px;"><p class="heading">{{ column[4].headerName }}</p><p /> </th>
                    <th scope="col" class="header-alignment" style="width: 400px;"><p class="heading">{{ column[5].headerName }}</p><p /> </th>
                    <th scope="col" class="header-alignment"> 
                        <p class="heading">{{ column[6].headerName }}</p>
                        <p class="sub-heading">{{ column[7].headerName }}</p>
                    </th>
                </template>
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