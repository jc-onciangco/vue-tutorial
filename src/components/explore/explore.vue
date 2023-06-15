<script lang="ts" setup>
import { onMounted, ref, watch, computed, reactive } from 'vue';
import BaseButton from '../for-tutorial/base-button.vue';
import TheLayout from './components/layout/social-media-layout.vue';
import ProfileBanner from './components/profile-banner.vue'
import ProfileGallery from './components/profile-gallery.vue'

const headerColumn = [
    {
        Url: 'Url',
        urlKey: 'url'
    }
];

const dataSource = ref(); 

const displayPicture = "src/components/explore/components/assets/cat-pic.jpg";

onMounted(async () => {
    const res = await fetch('https://jsonplaceholder.typicode.com/photos');
    const data = await res.json();

    dataSource.value = data;
});

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
            <ProfileGallery :data-source="dataSource" >

            </ProfileGallery>
        </div>
    </TheLayout>
</template>

<style lang="scss" scoped>
</style>