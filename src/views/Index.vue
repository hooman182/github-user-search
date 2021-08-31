<template>
  <div
    class="
      h-screen
      w-full
      lg:w-1/2
      p-5
      lg:p-0
      lg:m-auto
      flex flex-col
      items-center
      justify-center
    "
  >
    <TheHeader />
    <SearchBar @searchHandle="getSearchData" />
    <TheContent :userData="githubData" />
    <p
      class="text-gray-400 font-semibold text-lg"
      v-if="!githubData.data && !githubData.status"
    >
      Start searching in the github users
    </p>
    <p
      class="text-blue-400 font-semibold text-lg"
      v-if="githubData.status === 'searching'"
    >
      Searching...
    </p>
    <p class="text-red-400 font-semibold text-lg" v-if="githubData.error">
      {{ githubData.error }}
    </p>
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader";
import SearchBar from "@/components/SearchBar";
import TheContent from "@/components/TheContent";
import { reactive } from "@vue/runtime-core";
import axios from "axios";
export default {
  name: "Index",
  components: { TheHeader, SearchBar, TheContent },
  setup() {
    const githubData = reactive({
      data: null,
      status: null,
      error: null,
    });
    function getSearchData(data) {
      githubData.status = "searching";
      axios
        .get(`https://api.github.com/users/${data}`)
        .then((res) => {
          githubData.data = res.data;
          githubData.status = res.status;
        })
        .catch((err) => {
          githubData.error = err;
          githubData.status = null;
        });
    }

    return { githubData, getSearchData };
  },
};
</script>
