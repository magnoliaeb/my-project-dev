<template>
  <div class="bg-white shadow mb-2">
    <header class="px-4 py-2 flex justify-between items-center">
      <h2 class="text-lg font-mono font-bold">Listings</h2>
      <span class="text-xs text-primary-500 font-bold">
          <router-link :to="{ name: 'listings'}">See all</router-link>
      </span>
    </header>
    
    <template v-if="loading">
      <SkeletonItemList v-for="(item, index) in Array(4)" :key="item"  />

    </template>

    <template v-else>

      <div
        class="py-3 px-3 rounded-md text-base hover:bg-white mb-2"
        v-for="(item, index) in items"
        :key="index"
      >
        <nuxt-link
          class="leading-tight text-gray-700 hover:text-primary-500"
          :to="{ name: 'posts-id', params: { id: item.id } }"
        >
          <p>{{ item.title }}</p>
        </nuxt-link>
        <p v-if="item.comments_count" class="text-sm text-gray-500 mt-2">
          {{ item.comments_count }} comment
        </p>
        <span
          v-if="item.new"
          class="bg-primary-600 px-1 py-0.5 rounded-md text-white mt-1 inline-block text-xs"
          >new</span
        >
      </div>

    </template>
  </div>
</template>

<script>
import SkeletonItemList from './shared/SkeletonItemList.vue';

export default {
  components: { SkeletonItemList },

  async mounted() {
    await this.getPostsByTag();
  },
  props: {
    title: {
      type: String
    }
  },

  data() {
    return {
      items: [],
      loading: false
    };
  },

  methods: {
    async getPostsByTag() {
      this.loading = true

      const res = await this.$axios.get("/listings", {
        params: { tag: this.title, per_page: 5 }
      });

      this.items = res.data.map(item => {
        return {
          id: item.id,
          title: item.title,
          new: false,
          comments_count: item.comments_count,
          slug: item.slug
        }

      });

      this.loading = false
    }
    
  }
};
</script>

<style lang="scss" scoped></style>
