<script lang="ts" setup>
import type { Idatasource } from '@/components/explore/explore.vue'

defineProps<{
    imageTitle?: string;
}>();

</script>

<template>
    <div class="content-user">
        <div class="profile-card">
            <div class="profile-image">
                <img src="src/components/explore/components/assets/cat-pic.jpg" class="profile-image__img" />
            </div>
            <div class="profile-info">
                <h3>Miggy</h3>
            </div>
            <div class="image-description">
                <div class="image-description-date"><p class="image-description-date">January 1, 2023</p></div>
                <div class="image-description-title"><p>{{ imageTitle }}</p></div>
            </div>
        </div>
    </div>
</template>

<style lang="scss">
.profile-card {
    width: 100%;
    max-width: 700px;
    margin: 0 auto;
    padding: 1px;
    box-sizing: border-box;
    border-radius: 20px;
    background-color: #fff;
    overflow: hidden;
    position: relative;
    min-height: 150px;
    margin-bottom: 2rem;
}

.profile-card .profile-image__img {
    width: 10%;
    height: auto;
    border-radius: 50%;
    position: absolute;
    top: 30px;
    left: 30px;
}


.profile-info {
    width: 85%;
    float: right;
    padding-top: 35px;
    padding-left: 10px;
    box-sizing: border-box;
}

.image-description-date {
    width: 85%;
    float: left;
    padding-top: 10px;
    padding-left: 10px;
}

.image-description-title {
    width: 85%;
    float: left;
    padding-left: 20px;
}

.image-description-date {
    font-size: 0.9em;
}

.profile-info h3 {
    margin: 10px 0;
    font-weight: 700;
    font-size: 1.5em;
    color: #222;
}

.profile-info p {
    line-height: 140%;
    color: #666;
}

</style>