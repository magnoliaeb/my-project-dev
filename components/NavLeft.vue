<template>
  <ul class="space-y-1 bg-white z-50">
    <li
      class="text-gray-900 text-lg hover:text-primary-500 hover:bg-gray-200 lg:rounded py-1 lg:px-2 px-8"
      v-for="(link, index) in links"
      :key="index"
    >
      <router-link 
      :to="{ name: link.to }" 
      active-class="font-bold" exact
      class="flex items-center flex-none">
        <span class="h-4 w-4 bg-primary-200 inline-block mr-2 "></span>
        {{ link.name }}
      </router-link>
    </li>
    <li class="text-gray-500 text-sm ml-8 mt-4">More...</li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      links: [
        { name: "Home", to: "index", icon: "" },
        { name: "Sign In/Up", to: "auth", icon: "" },
        { name: "Listings", to: "listings", icon: "" },
        { name: "Podcasts", to: "podcasts", icon: "" },
        { name: "Videos", to: "videos", icon: "" },
        { name: "Tags", to: "tags", icon: "" }
      ]
    };
  }
};
</script>

<style scoped>
.router-link-active {
  font-weight: bold;
  color: red;
}
</style>
