<script lang="ts" setup>

</script>

<template>
    <GalleryModal ref="refGalleryModal">
        <template #title></template>
        <template #body-content></template>
    </GalleryModal>
    <v-skeleton-loader>
      
    </v-skeleton-loader>
    <slot name="user-gallery">
      <div class="gallery" id="gallery">
        <div class="image-container">
          <img />
        </div>
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