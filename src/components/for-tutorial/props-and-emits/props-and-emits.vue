<script lang="ts" setup>
import { ref } from 'vue';
import TheLayout from '../layouts/the-layout.vue';
import TheUser, { type IFriend } from './the-user.vue';
import BaseButton from '../base-button.vue';

interface IRemovedItemCache {
  index: number;
  removedItem: IFriend;
}

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
const removedItemCache = ref<IRemovedItemCache>();
const userName = ref();

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
  [...friends.value].forEach((friend, index) => {
    if (friend.id === id) {
      removedItemCache.value = {
        index,
        removedItem: friend
      };
    }
  });

  friends.value = [...friends.value].filter((friend) => {
    return friend.id !== id;
  });
};

const handleClickUndoRemovedItem = () => {
  const removedItemIndex = removedItemCache.value?.index;
  const removedItem = removedItemCache.value?.removedItem;

  if (removedItemIndex !== undefined && removedItem) {
    friends.value.splice(removedItemIndex, 0, removedItem);

    removedItemCache.value = undefined;
  }
};

const handleAddUser = () => {
  const newUser = {
    id: Math.random(),
    name: userName.value
  };

  friends.value.unshift(newUser);
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
        :has-removed-item-cached="Boolean(removedItemCache)"
        @on-remove-friend="handleClickRemoveFriend"
        @on-undo-removed-item="handleClickUndoRemovedItem"
      />

      <BaseButton :color="'danger'" @click="refTheUser?.hideAllFriends()">
        <template #label
          >{{ refTheUser?.areAllFriendsHide ? 'Show' : 'Hide' }} All Friends
        </template>
      </BaseButton>

      <div>
        <input type="text" class="form-control" placeholder="Add User" v-model="userName" />
        <BaseButton :color="'primary'" class="w-100 mt-2" @click="handleAddUser">
          <template #label>Add User </template>
        </BaseButton>
      </div>
    </div>
  </TheLayout>
</template>

<style lang="scss" scoped></style>
