<template>
  <div
    class="
      h-screen
      w-full
      lg:w-1/2
      pt-6
      px-2.5
      lg:p-0
      lg:m-auto
      flex flex-col
      items-center
      justify-start
      lg:justify-center
    "
  >
    <TheHeader />
    <SearchBar @searchHandle="getSearchData" />
    <TheContent :userData="githubData" />
    <Messages :message="computeMessage" />
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader";
import SearchBar from "@/components/SearchBar";
import TheContent from "@/components/TheContent";
import Messages from "@/components/Messages";
import { computed, reactive } from "@vue/runtime-core";
import axios from "axios";
export default {
  name: "Index",
  components: { TheHeader, SearchBar, TheContent, Messages },
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
          githubData.status = "Error";
        });
    }
    const computeMessage = computed(() => {
      let message = {};
      switch (githubData.status) {
        case "Error":
          message = {
            text: githubData.error,
            status: 0,
          };
          break;
        case "searching":
          message = {
            text: "Searching...",
            status: 1,
          };
          break;
        case 200:
          message = {
            text: "",
            status: 200,
          };
          break;
        default:
          message = {
            text: "Start searching in the github users",
            status: -1,
          };
          break;
      }
      return message;
    });

    return { githubData, getSearchData, computeMessage };
  },
};
</script>
