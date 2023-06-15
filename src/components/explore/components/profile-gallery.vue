<script lang="ts" setup>
import { ref } from 'vue';
import GalleryModal from './gallery-modal.vue';

export interface Iimages {
    imgUrl: 'Url',
    imgUrlKey: 'url'
}

const refGalleryModal = ref<InstanceType<typeof GalleryModal>>();

defineProps<{
    dataSource: Record<Iimages['imgUrlKey'], any>[]
}>();

const handleClickShowGalleryModal = () => {
    refGalleryModal.value?.showModal();
};

</script>

<template>
    <GalleryModal ref="refGalleryModal">
        <template #title>IMG Title</template>
        <template #body-content>Img Content</template>
    </GalleryModal>

    <slot name="user-gallery">
        <div class="gallery" id="gallery">
            <div v-for="data in dataSource" class="image image-container">
                <img :src="data.url" @click="handleClickShowGalleryModal()">
            </div>
        </div>
    </slot>
</template>

<style lang="scss">
.gallery {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
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