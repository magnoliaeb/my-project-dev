<template>
 
    <!-- <pre>{{ podcast }}</pre> -->

    <article v-if="podcast" class="flex p-4 border-b bg-white lg:rounded lg:shadow-md lg:mb-3">
      <img
        class="w-10 h-10 bg-primary-500 rounded-full flex-none mr-4"
        :src="podcast.image_url"
        alt=""
      />
      <div class="flex-grow">
        <h2 class="text-xl md:text-2xl font-bold leading-tight mb-2">
          <span class="bg-primary-500 text-white text-sm rounded px-1 py-0.5"
            >podcast</span
          >
          {{ podcast.title }}
        </h2>
           <nuxt-link  :to="{ name: 'podcasts-slug', params: { slug: podcast.podcast.slug } }" class="">
            <p v-if="podcast.podcast" class="text-gray-500 font-semibold text-sm hover:underline" v-html="podcast.podcast.title">
              
            </p>
        </nuxt-link>
      </div>
    </article>
</template>

<script>
export default {
  props: {
    podcast: {
      type: Object
    }
  }
};
</script>

<style lang="scss" scoped></style>
