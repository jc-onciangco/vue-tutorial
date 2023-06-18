<script lang="ts" setup>
import { onMounted, ref, watch, computed, reactive } from 'vue';
import BaseButton from '../for-tutorial/base-button.vue';
import TheLayout from './components/layout/social-media-layout.vue';
import ProfileBanner from './components/profile-banner.vue';
import ProfileGallery from './components/profile-gallery.vue';

const headerColumn = [
  {
    Url: 'Url',
    urlKey: 'url'
  }
];

const dataSource = ref();
const currentPage = ref(1);

const displayPicture = 'src/components/explore/components/assets/cat-pic.jpg';

const fetchApi = async () => {
  // const res = await fetch(
  //   `https://jsonplaceholder.typicode.com/photos?_page=${currentPage.value}&_limit=10`
  // );
  const res = await fetch(`api/accounts/ledger?contractno=1`);
  const data = await res.json();
  console.log('data:', data);
  return data;
};

onMounted(async () => {
  dataSource.value = await fetchApi();
});

const handleClickNextPage = () => currentPage.value++;

watch(
  () => currentPage.value,
  async (newValue) => {
    dataSource.value = await fetchApi();
  }
);
</script>

<template>
  <TheLayout>
    <div>
      <ProfileBanner :src="displayPicture">
        <template #user-img></template>
        <template #user-name> Miggy </template>
      </ProfileBanner>
    </div>
    <div>
      <ProfileGallery :data-source="dataSource"></ProfileGallery>
      <div class="d-flex justify-content-between align-items-center px-4">
        <BaseButton color="primary">
          <template #label>PREV</template>
        </BaseButton>
        <BaseButton color="primary" @click="handleClickNextPage">
          <template #label>NEXT</template>
        </BaseButton>
      </div>
    </div>
  </TheLayout>
</template>

<style lang="scss" scoped></style>
