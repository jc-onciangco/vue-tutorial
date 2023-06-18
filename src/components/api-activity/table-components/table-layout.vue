<script lang="ts" setup>
import type { Iledgerdata } from '../api-activity.vue';
import dayjs from 'dayjs';
import TablePopper from './table-popper.vue';


defineProps<{
    dataSource?: Iledgerdata[]
}>();

const rowHeaders = [
    {
        rowHeaderName: "Account Name"
    },
    {
        rowHeaderName: "Account Code"
    },
    {
        rowHeaderName: "Account Type"
    },
    {
        rowHeaderName: "Period Covered"
    },
    {
        rowHeaderName: "Anniversary Date"
    },
    {
        rowHeaderName: "Billing Schedule"
    },
    {
        rowHeaderName: "Mother Account"
    },
    {
        rowHeaderName: "Address"
    },
    {
        rowHeaderName: "Office No"
    },
    {
        rowHeaderName: "Website"
    }
];
const handlePolicyDateConversion = (fromDate: Date, toDate: Date) => {
    const from = dayjs(fromDate).format('MM/DD/YYYY');
    const to = dayjs(toDate).format('MM/DD/YYYY');
    const combinedString = from + " - " + to;
    return combinedString;
}

const handleEncodedDateConversion = (encodedDate: Date) => {
    return dayjs(encodedDate).format('MM/DD/YYYY');
}

const handleEmptyStrings = (data: string) => {
    if (data === "") {
        return "NOT SPECIFIED";
    } else {
        return data;
    }
}

const handleAddress = (street: string, city:string, province: string) => {
    return handleEmptyStrings(street + " " + city + " " + province)
}

</script>

<template>
    <slot>
        <table class="table table-light table-striped">
            <thead>
                <tr>
                    <slot name="table-col-header"></slot>
                </tr>
            </thead>
            <tbody>
                <tr v-for="data in dataSource" :key="data.contractno">
                    <th scope="row" style="width: 150px; text-align: center;">
                        <TablePopper placement="right">
                            <img src="@/assets/information.png" class="icon-size">
                            <template #content>
                                <div style="width: 40rem;">
                                    <div></div>
                                    <div style="padding: 20px">
                                        <table class="table table-light">
                                            <thead>
                                                <tr>
                                                    <td class="header-style" colspan="3" style="color: #207068; font-weight: bold;">
                                                        CORPORATE PROFILE DETAILS
                                                    </td></tr>
                                            </thead>
                                            <tbody>
                                                <!-- Account Name -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[0].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEmptyStrings(data.companyname) }}</td>
                                                </tr>
                                                <!-- Account Code -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[1].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEmptyStrings(data.contractno) }}</td>
                                                </tr>
                                                <!-- Account Type -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[2].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEmptyStrings(data.accounttypedesc) }}</td>
                                                </tr>
                                                <!-- Period Covered -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[3].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handlePolicyDateConversion(data.effectivity, data.expiry) }}</td>
                                                </tr>
                                                <!-- Anniversary Date -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[4].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEncodedDateConversion(data.dateenrolled) }}</td>
                                                </tr>
                                                <!-- Billing Schedule -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[5].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEmptyStrings(data.billingschedulename) }}</td>
                                                </tr>
                                                <!-- Mother Account -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[6].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEmptyStrings(data.motheraccount) }}</td>
                                                </tr>
                                                <!-- Address -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[7].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleAddress(data.streetaddress, data.cityname, data.provincename) }}</td>
                                                </tr>
                                                <!-- Office No. -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[8].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEmptyStrings(data.mothercontractno) }}</td>
                                                </tr>
                                                <!-- Website -->
                                                <tr>
                                                    <th class="cell-size-col1">{{ rowHeaders[9].rowHeaderName }}</th>
                                                    <td class="cell-size-col2">{{ ":" }}</td>
                                                    <td class="cell-size-col3">{{ handleEmptyStrings(data.website) }}</td>
                                                </tr>
                                            </tbody>
                                        </table>
                                        <div class="footer-btn">
                                            <button class="view-btn">View More</button>
                                        </div>
                                    </div>
                                </div>
                            </template>
                        </TablePopper>
                    </th>
                        <!-- Account Name Code -->
                        <td class="cell-style">
                            <p class="heading">{{ data.companyname}}</p>
                            <p class="sub-heading">{{ data.contractno }}</p>
                        </td>
                        <!-- S -->
                        <td class="cell-style"><span class="badge text-bg-success">{{ data.statusintial }}</span></td>
                        <!-- Policy Period -->
                        <td class="cell-style"><p class="cell-style-gray">{{ handlePolicyDateConversion(data.effectivity, data.expiry) }}</p></td>
                        <!-- Address -->
                        <td class="cell-style"><p class="cell-style-gray">{{  data.streetaddress + " " + data.cityname + " " + data.provincename }}</p></td>
                        <!-- Encoded By Date Encoded -->
                        <td class="cell-style">
                            <p class="heading">{{ handleEmptyStrings(data.encodedbyname) }}</p>
                            <p class="sub-heading">{{ handleEncodedDateConversion(data.dateencoded) }}</p>
                        </td>
                </tr>
            </tbody>
        </table>
    </slot>
</template>

<style scoped>
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
    background-image: linear-gradient(to top, #F2994A  43%,#F2C94C  100%);
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