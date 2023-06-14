<script lang="ts" setup>
const props = defineProps<{
    src?: string
}>();

</script>

<template>
    <div class="container drop-shadow">
        <div>
        <slot name="user-img">
            <img :src=src class="rounded-corners" />
        </slot>
        </div>
        <div class="item details">
            <slot name="user-name"></slot>
        </div>
    </div>
</template>

<style lang="scss">
img.rounded-corners {
  border-radius: 50%;
  width: 100px;
  height: 100px;
}

.container {
    display: flex;
    border-radius: 5px;
    width: 30rem;
}

.item {
    flex: 1;
}

.details {
    display: flex;
    justify-content: center;
    align-items: center;
}

.drop-shadow {
    border: 1px solid;
    padding: 10px;
    box-shadow: 4px 3px;
}
</style>