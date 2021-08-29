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
    <SearchBar />
  </div>
</template>

<script>
import TheHeader from "@/components/TheHeader";
import SearchBar from "@/components/SearchBar";
export default {
  name: "Index",
  components: { TheHeader, SearchBar },
};
</script>
