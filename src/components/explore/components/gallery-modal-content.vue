<script lang="ts" setup>
import { ref, watch } from 'vue';
import type { Idatasource } from '../explore.vue';
import ModalImageDescription from './modal-components/modal-image-description.vue'
import ModalCommentSection from './modal-components/modal-comment-section.vue'

defineProps<{
  dataSource?: Idatasource;
}>();


</script>

<template>
  <div class="card-container">
    <div class="card">
      <div class="content">
        <div class="image-section">
          <slot name="image-slot">
            <div>
              <img class="image-size" :src="dataSource?.url"/>
            </div>
          </slot>
        </div>
        <div class="content-section">
          <ModalImageDescription :image-title="dataSource?.title">
          </ModalImageDescription>
        </div>

          <div class="content-comment">
            <ModalCommentSection></ModalCommentSection>
          </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.custom-modal {
  //   min-height: 500px;
  background-color: white;
}

.card-container {
  display: grid;
  grid-template-columns: repeat(0, 1fr);
  margin: auto;
  height: 31rem;
  width: 60rem;
}

.card {
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  height: 100%;
}

.content {
  padding-left: 10px;
  padding-top: 10px;
  max-height: 100%;
}

.image-section {
  float: left;
  width: 50%;
}

.content-section {
  display: grid;
  float: left;
  width: 50%;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr;
  gap: 0px 0px;
}

.content-user {
  height: 50%;
  padding-bottom: 1%;
}

.content-comment {
  height: 50%;
}

.image-size {
  width: 100%;
  max-height: 100%;
}

</style>
