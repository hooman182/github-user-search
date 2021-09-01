<template>
  <div
    class="
      w-full
      p-6
      bg-white
      dark:bg-opacity-10
      rounded-lg
      grid grid-cols-4
      gap-5
    "
    v-if="userData.data && userData.status==200"
  >
    <!-- start header -->
    <div class="grid grid-cols-4 gap-x-5 col-start-1 col-end-5 row-span-1">
      <div class="col-span-1">
        <img
          :src="userData.data.avatar_url"
          :alt="userData.data.name + 'image'"
          class="rounded-full"
        />
      </div>

      <div class="grid grid-cols-1 gap-2 col-start-2 col-end-5">
        <div class="grid grid-cols-1 lg:grid-cols-2 items-center">
          <h1
            class="text-2xl font-bold text-gray-700 dark:text-gray-200 order-1"
          >
            {{ userData.data.name }}
          </h1>
          <p class="text-gray-400 order-3 lg:order-2">
            Joined {{ userData.data.created_at.slice(0, 10) }}
          </p>
          <a
            :href="'https://github.com/' + userData.data.login"
            class="text-blue-500 font-medium order-2 lg:order-3"
            target="_blank"
          >
            @{{ userData.data.login }}
          </a>
        </div>

        <p class="hidden lg:block text-gray-400 dark:text-gray-300 font-medium">
          <span
            class="text-gray-400 dark:text-gray-500"
            v-if="!userData.data.bio"
            >Bio doesn't exist</span
          >
          {{ userData.data.bio }}
        </p>
      </div>
      <p
        class="
          lg:hidden
          col-start-1 col-end-5
          text-gray-400
          dark:text-gray-300
          font-medium
        "
      >
        {{ userData.data.bio }}
      </p>
    </div>
    <!-- end header -->
    <!-- start body -->
    <div
      class="
        bg-gray-100
        dark:bg-gray-800
        rounded-md
        px-6
        py-2
        col-start-1 col-end-5
        lg:col-start-2 lg:col-end-5
        row-span-2
        grid grid-cols-3
      "
    >
      <div class="flex flex-col">
        <span class="font-medium text-gray-400 text-center lg:text-left"
          >Repos</span
        >
        <span class="font-bold dark:text-white text-center lg:text-left">{{
          userData.data.public_repos
        }}</span>
      </div>
      <div class="flex flex-col">
        <span class="font-medium text-gray-400 text-center lg:text-left"
          >Followers</span
        >
        <span class="font-bold dark:text-white text-center lg:text-left">{{
          userData.data.followers
        }}</span>
      </div>
      <div class="flex flex-col">
        <span class="font-medium text-gray-400 text-center lg:text-left"
          >Following</span
        >
        <span class="font-bold dark:text-white text-center lg:text-left">{{
          userData.data.following
        }}</span>
      </div>
    </div>
    <!-- end body -->
    <!-- start footer -->
    <div
      class="
        col-start-1 col-end-5
        lg:col-start-2 lg:col-end-5
        row-span-3
        grid grid-cols-1
        lg:grid-cols-2
        gap-3
      "
    >
      <span class="flex items-center">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mr-2 text-gray-500 dark:text-white"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z"
            clip-rule="evenodd"
          />
        </svg>
        <span
          class="text-gray-500 dark:text-gray-300"
          v-if="userData.data.location"
        >
          {{ userData.data.location }}
        </span>
        <span class="text-gray-500 dark:text-gray-300" v-else
          >Not Available</span
        >
      </span>
      <span class="flex items-center">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-6 w-6 mr-2 text-gray-500 dark:text-white"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
        >
          <path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1"
          />
        </svg>
        <a
          :href="userData.data.blog"
          class="text-gray-500 dark:text-gray-300 truncate"
          v-if="userData.data.blog"
          >{{ userData.data.blog }}</a
        >
        <span class="text-gray-500 dark:text-gray-300" v-else
          >Not Available</span
        >
      </span>
      <span class="flex items-center">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5 mr-2 text-gray-500 dark:text-white"
          viewBox="0 0 20 20"
          fill="currentColor"
        >
          <path
            fill-rule="evenodd"
            d="M4 4a2 2 0 012-2h8a2 2 0 012 2v12a1 1 0 110 2h-3a1 1 0 01-1-1v-2a1 1 0 00-1-1H9a1 1 0 00-1 1v2a1 1 0 01-1 1H4a1 1 0 110-2V4zm3 1h2v2H7V5zm2 4H7v2h2V9zm2-4h2v2h-2V5zm2 4h-2v2h2V9z"
            clip-rule="evenodd"
          />
        </svg>
        <span
          class="text-gray-500 dark:text-gray-300"
          v-if="userData.data.company"
        >
          @{{ userData.data.company }}
        </span>
        <span class="text-gray-500 dark:text-gray-300" v-else>
          Not Available
        </span>
      </span>
    </div>
    <!-- end footer -->
  </div>
</template>

<script>
export default {
  name: "TheContent",
  props: {
    userData: {
      type: Object,
      required: true,
    },
  },
};
</script>
