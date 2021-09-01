<template>
  <form method="post" class="w-full my-4" @submit.prevent="searchFormHandle">
    <div class="bg-white dark:bg-opacity-10 flex items-center rounded-lg p-2">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-5 w-5 lg:h-6 lg:w-6 lg:ml-2 text-blue-500"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
        />
      </svg>
      <input
        type="text"
        placeholder="Search github username..."
        class="
          bg-white bg-opacity-0
          flex-1
          mx-4
          outline-none
          font-semibold
          dark:text-gray-400
        "
        v-model="searchValue"
      />
      <button type="submit" class="btn-blue">Search</button>
    </div>
  </form>
</template>

<script>
import { ref } from '@vue/reactivity';
export default {
  name:"SearchBar",
  setup(props, {emit}) {
    const searchValue = ref('');
    function searchFormHandle() {
      emit('searchHandle', searchValue.value);
      searchValue.value = "";
    }
    return{searchValue, searchFormHandle}
  }
};
</script>