<template>
  <p class="font-semibold text-lg" :class="messageColor">
    {{ message.text }}
  </p>
</template>

<script>
import { computed } from "@vue/reactivity";
export default {
  name: "Messages",
  props: ["message"],
  setup(props) {
    
    const messageColor = computed(() => {
      let setTextColor = {};
      switch (props.message.status) {
        case 0:
          setTextColor = {
            "text-red-400": true,
            "text-blue-400": false,
          };
          break;

        default:
          setTextColor = {
            "text-red-400": false,
            "text-blue-400": true,
          };
          break;
      }
      return setTextColor;
    });

    return { messageColor };
  },
};
</script>

<style>
</style>