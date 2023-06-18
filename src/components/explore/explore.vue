<script lang="ts" setup>
import { onMounted, ref, watch, computed, reactive } from 'vue';
import BaseButton from '../for-tutorial/base-button.vue';
import TheLayout from './components/layout/social-media-layout.vue';
import ProfileBanner from './components/profile-banner.vue';
import ProfileGallery from './components/profile-gallery.vue';
import ProfileBannerSkeleton from './components/layout/profile-banner-skeleton.vue';

export interface Idatasource {
  albumId: number;
  id: number;
  title: string;
  url: string;
  thumbnailUrl: string;
}

const headerColumn = [
  {
    Url: 'Url',
    urlKey: 'url'
  }
];

const dataSource = ref<Idatasource>();
const currentPage = ref(1);
const isPrevDisabled = ref(true);
const isNextDisabled = ref(false);
const displayPicture = 'src/components/explore/components/assets/cat-pic.jpg';
const isLoading = ref(false);

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

const handleFetchApi = async () => {
  isLoading.value = true;
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/photos?_page=${currentPage.value}&_limit=10`
  );
  const data = await res.json();
  isLoading.value = false;
  dataSource.value = data;
};

onMounted(async () => {
  handleFetchApi();
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
    <div v-if="isLoading">Loading. . .</div>
    <div v-else>
      <ProfileGallery :data-source="dataSource"></ProfileGallery>
      <div class="pagination">
        <div
          class="pagination-button"
          :class="isPrevDisabled ? 'disabled-button' : 'active-button'"
          @click="handleClickPrev"
        >
          {{ '< Prev' }}
        </div>
        <div
          class="pagination-button"
          :class="isNextDisabled ? 'disabled-button' : 'active-button'"
          @click="handleClickNext"
        >
          {{ 'Next >' }}
        </div>
      </div>
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

<style lang="scss" scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-left: 9rem;
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
</style>
