<script lang="ts" setup>
const props = defineProps<{
    src?: string
}>();

</script>

<template>
    <div class="profile-card">
        <div class="profile-image">
        <slot name="user-img">
            <img :src=src class="profile-image__img" />
        </slot>
        </div>
        <div class="profile-info">
            <span>Profile of:</span>
            <h3><slot name="user-name"></slot></h3>
            <p>User Bio</p>
        </div>
    </div>
</template>

<style lang="scss">
.profile-card {
    width: 100%;
    max-width: 700px;
    margin: 0 auto;
    padding: 30px;
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
    padding-left: 10px;
    box-sizing: border-box;
}

.profile-info span {
    text-transform: uppercase;
    color: #666;
    letter-spacing: 3px;
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