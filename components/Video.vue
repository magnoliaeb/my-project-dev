<template>
  <!-- col -->
  <div class="mb-4 full-width md:w-1/2 p-1 lg:w-1/3">
    <!-- video -->
    <article class="shadow-lg bg-white">
      <div class="relative">
        <img
          :src="video.cloudinary_video_url"
          class="h-72 border object-cover"
          :alt="video.title"
        />
        <span
          class="bg-gray-800 text-white absolute right-2 bottom-4 px-2 py-0.5 font-medium rounded-md text-sm bg-opacity-40"
          >{{ video.video_duration_in_minutes }}</span
        >
      </div>
      <div class="px-4 py-2">
        <h2
          class="text-lg font-bold leading-tight truncate"
          v-html="video.title"
        ></h2>
        <p class="text-gray-500 mt-2">{{ video.user.name }}</p>
      </div>
    </article>
  </div>
</template>

<script>
export default {
  props: {
    video: {
      type: Object
    }
  }
};
</script>

<style lang="scss" scoped></style>
