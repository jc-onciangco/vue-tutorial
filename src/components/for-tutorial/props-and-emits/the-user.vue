<script lang="ts" setup>
import { ref } from 'vue';

export interface IFriend {
  id: number;
  name: string;
}

const props = defineProps<{
  name: string;
  age: number;
  isOnline: boolean;
  friends?: IFriend[];
}>();

const emit = defineEmits<{
  (e: 'onRemoveFriend', id: IFriend['id']): void;
  (e: 'onUndoRemovedItem', id: number): void;
}>();

const areAllFriendsHide = ref<boolean>(false);
const removedItemCache = ref<number>(0);

const handleClickRemove = (id: IFriend['id']) => {
  removedItemCache.value = id;

  emit('onRemoveFriend', id);
};

const hideAllFriends = () => {
  areAllFriendsHide.value = !areAllFriendsHide.value;
};

const handleClickUndoRemovedItem = () => {
  emit('onUndoRemovedItem', removedItemCache.value);

  removedItemCache.value = 0;
};

defineExpose({
  areAllFriendsHide,
  hideAllFriends
});
</script>

<template>
  <div class="d-flex flex-column gap-3">
    <div class="d-flex flex-column gap-2">
      <div>name: {{ name }}</div>
      <div>age: {{ age }}</div>
      <div>is online: {{ isOnline }}</div>
    </div>
    <div>
      <div class="d-flex align-items-center justify-content-between">
        <div>Friends</div>
        <button v-if="removedItemCache" @click="handleClickUndoRemovedItem">Undo</button>
      </div>
      <div v-if="friends && !areAllFriendsHide" class="d-flex flex-column gap-2">
        <template v-for="(friend, index) in friends" :key="friend.id">
          <div
            class="d-flex align-items-center justify-content-between gap-2 bg-success bg-opacity-10 py-1 px-2"
          >
            <div>{{ index }} - {{ friend.name }}</div>
            <button
              type="button"
              class="btn btn-sm btn-danger"
              @click="handleClickRemove(friend.id)"
            >
              Remove
            </button>
          </div>
        </template>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped></style>
