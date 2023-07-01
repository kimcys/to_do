<template>
  <div class="flex-col mx-auto content-center justify-center w-96 rounded-xl">

    <div class="my-20 rounded-md">

      <div class="col-span-2 justify-center content-center">
        <h1 class="font-semibold text-2xl font-mono text-center my-3">Warung Pak Ngah Order List</h1>
      </div>

      <div class="flex justify-center content-center my-5">
        <form @submit.prevent="addItem">
          <input
            class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
            type="text" v-model="newItem" placeholder="Add New Item" />
        </form>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-xl justify-center mx-3"
          type="submit" @click="addItem()">
          ADD</button>
      </div>

      <div class="col-span-2">
        <ul>
          <li v-for="(item, index) in items" :key="index" class="m-2">
            <input type="checkbox" class="mx-3" v-model="item.completed" />
            <span :class="{ completed: item.completed }">{{ item.text }}</span>
            <button class="bg-red-500 hover:bg-red-700 text-white font-bold py-2 px-4 rounded-xl mx-5"
              @click="deleteItem(index)">Delete</button>
          </li>
        </ul>
      </div>

    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

export default {

  setup() {
    const items = ref([
      { text: 'Roti Canai x2', completed: false },
      { text: 'Nasi Lemak Telur Mata x4', completed: false },
      { text: 'Nasi Goreng Cina x2', completed: false },
    ]);

    const newItem = ref('');

    function addItem() {
      if (newItem.value.trim() !== '') {
        items.value.push({
          text: newItem.value.trim(),
          completed: false,
        });
        newItem.value = '';
      }
    }

    function deleteItem(index) {
      items.value.splice(index, 1);
    }

    return {
      items,
      newItem,
      addItem,
      deleteItem,
    };
  },
};
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>
