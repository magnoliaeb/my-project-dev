<template>
  <div class="h-screen">
    <div class="md:flex pt-4">
      <div class="hidden md:block lg:w-1/4 w-1/3 px-4">
        <NavListingLeft />
      </div>

      <div class="md:w-2/3 lg:w-2/3 bg md:px-4">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "Listings"
    };
  },
  head() {
    return {
      title: this.title,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Listing page description"
        }
      ]
    };
  }
};
</script>
