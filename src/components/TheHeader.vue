<template>
  <header class="w-full flex justify-between items-center mb-3">
    <h1 class="text-lg md:text-xl font-bold text-gray-600 dark:text-white">
      Github users finder
    </h1>
    <button
      class="btn"
      @click="themeMode"
    >
      {{ darkMode }}
      <template v-if="darkMode == 'Dark'">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 ml-2"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            d="M17.293 13.293A8 8 0 016.707 2.707a8.001 8.001 0 1010.586 10.586z"
          />
        </svg>
      </template>
      <template v-else>
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 ml-2"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M10 2a1 1 0 011 1v1a1 1 0 11-2 0V3a1 1 0 011-1zm4 8a4 4 0 11-8 0 4 4 0 018 0zm-.464 4.95l.707.707a1 1 0 001.414-1.414l-.707-.707a1 1 0 00-1.414 1.414zm2.12-10.607a1 1 0 010 1.414l-.706.707a1 1 0 11-1.414-1.414l.707-.707a1 1 0 011.414 0zM17 11a1 1 0 100-2h-1a1 1 0 100 2h1zm-7 4a1 1 0 011 1v1a1 1 0 11-2 0v-1a1 1 0 011-1zM5.05 6.464A1 1 0 106.465 5.05l-.708-.707a1 1 0 00-1.414 1.414l.707.707zm1.414 8.486l-.707.707a1 1 0 01-1.414-1.414l.707-.707a1 1 0 011.414 1.414zM4 11a1 1 0 100-2H3a1 1 0 000 2h1z"
            clip-rule="evenodd"
          />
        </svg>
      </template>
    </button>
  </header>
</template>

<script>
import { ref } from "@vue/reactivity";
import { onBeforeMount } from "@vue/runtime-core";
export default {
  name: "TheHeader",
  setup() {
    const darkMode = ref("Dark");
    function themeMode() {
      if (localStorage.theme == "" || localStorage.theme == undefined) {
        document.documentElement.classList.add("dark");
        localStorage.setItem("theme", "dark");
        darkMode.value = "Light";
      } else {
        document.documentElement.classList.remove("dark");
        localStorage.removeItem("theme");
        darkMode.value = "Dark";
      }
    }
    onBeforeMount(() => {
      if (localStorage.theme == "dark") {
        document.documentElement.classList.add("dark");
        darkMode.value = "Light";
      }
    });
    return { themeMode, darkMode };
  },
};
</script>
