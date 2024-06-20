<script lang="ts" setup>
import { ref, watch, computed, reactive } from 'vue';
import BaseButton from './base-button.vue';
import TheLayout from './layouts/the-layout.vue';

//refs with initial value
const counter = ref(0);

const boxDefaultSize = ref(20);
const boxScale = ref(1);

const userForms = reactive({
  username: 'Juan',
  password: 'Password@2'
});

const textMessage = ref('Hello, world!');

const boxPixel = computed(() => {
  return boxScale.value * boxDefaultSize.value;
});

// const addBy3 = computed(() => {
//   return counter.value + 3;
// });

const handleClickIncrement = (step?: number) => {
  if (step) {
    counter.value += step;
  } else {
    counter.value++;
  }
};

function handleClickDecrement() {
  if (counter.value === 0) {
    return alert('The minimum counter is zero!');
  }

  counter.value--;
}

watch(
  () => counter.value,
  (newVal, oldVal) => {
    boxScale.value = newVal;
  }
);
</script>

<template>
  <TheLayout>
    <div>
      <div v-if="false">
        Use Double Curly Braces to render the data from js to html.
        <span class="fw-semibold text-success">{{ textMessage }}</span>
      </div>

      <!-- <div>ADD BY 3</div> -->

      <div class="mt-2">
        <div
          class="blue-box d-flex align-items-center justify-content-center"
          :style="{ height: `${boxPixel}px`, aspectRatio: '1/1' }"
          @dblclick="counter = 1"
        ></div>

        <div class="mt-2">
          Click increment to scale-up the box size in
          <span class="fw-bold text-success">{{ boxPixel }}px</span>. Double click the box to reset
          to default
        </div>
      </div>

      <br />

      <div><span class="fw-semibold">The Counter: </span>{{ counter }}</div>
      <div class="d-flex gap-2 mt-2">
        <BaseButton @click="handleClickIncrement()">
          <template #label> Increment </template>
          <template #left-icon>
            <i class="bi bi-plus"></i>
          </template>
        </BaseButton>

        <BaseButton :color="'secondary'" @click="handleClickDecrement">
          <template #label> Decrement </template>
          <template #left-icon>
            <i class="bi bi-dash"></i>
          </template>
        </BaseButton>

        <BaseButton :color="'info'" @click="handleClickIncrement(5)">
          <template #label> Increment By </template>
          <template #left-icon>
            <i class="bi bi-plus"></i>
          </template>
          <template #right-icon>
            <i class="bi bi-5-circle-fill"></i>
          </template>
        </BaseButton>

        <BaseButton :color="'secondary'" @click="counter = 1">
          <template #label> Reset </template>
        </BaseButton>
      </div>

      <br />
      <br />

      <div><span class="fw-semibold">Box Size: </span>{{ boxDefaultSize }}</div>
      <div class="mt-2">
        <input type="text" v-model="boxDefaultSize" class="text-end form-control" />
      </div>

      <br />

      <div><span class="fw-semibold">Box Scale: </span>{{ boxScale }}</div>
      <div class="mt-2"><input type="text" v-model="boxScale" class="text-end form-control" /></div>
    </div>
  </TheLayout>
</template>

<style lang="scss" scoped>
.blue-box {
  background-color: blue;
  transition: all 0.2s linear;

  &:hover {
    background-color: orange;
  }
}
</style>
