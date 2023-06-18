<script lang="ts" setup>
import { ref, nextTick } from 'vue';
import GalleryModal from './gallery-modal.vue';
import type { Idatasource } from '../explore.vue';


export interface Iimages {
    imgUrl: 'Url',
    imgUrlKey: 'url'
}

const refGalleryModal = ref<InstanceType<typeof GalleryModal>>();
defineProps<{
    dataSource?: Idatasource[]
}>();

const selectedDataSource = ref<Idatasource>();

const handleClickShowGalleryModal = (data: Idatasource) => {
    selectedDataSource.value = data;
    nextTick();
    refGalleryModal.value?.showModal();
};

</script>

<template>
    <slot name="user-gallery">
      <div class="gallery" id="gallery">
        <div v-for="data in dataSource" class="image-container">
          <img :src="data.url" @click="handleClickShowGalleryModal(data)">
          
        </div>
        <GalleryModal ref="refGalleryModal" :data-source="selectedDataSource">
          <template #image-slot></template>
        </GalleryModal>
      </div>
    </slot>
</template>

<style lang="scss">
.gallery {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  width: 500px;
  margin-left: auto;
  margin-right: auto;
}

.gallery .image {
  width: 200px;
  height: 200px;
  margin: 10px;
  overflow: hidden;
}

.gallery .image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.image-container img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease; /* Apply a smooth transition effect */
}

.image-container:hover img {
  transform: scale(1.2); /* Increase the scale to enlarge the image */
}
</style>