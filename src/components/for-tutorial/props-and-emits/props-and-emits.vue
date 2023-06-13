<script lang="ts" setup>
import { ref } from 'vue';
import TheLayout from '../layouts/the-layout.vue';
import TheUser, { type IFriend } from './the-user.vue';
import BaseButton from '../base-button.vue';

const refTheUser = ref<InstanceType<typeof TheUser>>();

const initialValue = [
  {
    id: 1,
    name: 'Elon'
  },
  {
    id: 2,
    name: 'Jeff'
  },
  {
    id: 3,
    name: 'Bill'
  }
];

const friends = ref(initialValue);

// const friends = [
//   {
//     id: 0,
//     name: 'Elon'
//   },
//   {
//     id: 1,
//     name: 'Jeff'
//   },
//   {
//     id: 1,
//     name: 'Bill'
//   }
// ]

const handleClickRemoveFriend = (id: IFriend['id']) => {
  friends.value = [...friends.value].filter((friend) => {
    return friend.id !== id;
  });
};

const handleClickUndoRemovedItem = (id: number) => {
  const cachedItem = initialValue.find((friend) => {
    return friend.id === id;
  });

  friends.value.push(cachedItem);
};
</script>

<template>
  <TheLayout>
    <div class="d-flex flex-column gap-4">
      <TheUser
        ref="refTheUser"
        :name="'Mark'"
        :age="20"
        is-online
        :friends="friends"
        @on-remove-friend="handleClickRemoveFriend"
        @on-undo-removed-item="handleClickUndoRemovedItem"
      />

      <BaseButton :color="'danger'" @click="refTheUser?.hideAllFriends()">
        <template #label
          >{{ refTheUser?.areAllFriendsHide ? 'Show' : 'Hide' }} All Friends
        </template>
      </BaseButton>
    </div>
  </TheLayout>
</template>

<style lang="scss" scoped></style>
