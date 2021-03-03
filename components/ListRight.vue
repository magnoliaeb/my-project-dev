<template>
  <div class="bg-white shadow mb-2">
    <header class="px-4 py-2">
      <h2 class="text-lg font-mono font-bold">#{{ title }}</h2>
    </header>

    <template v-if="loading">
      <SkeletonItemList  v-for="(item, index) in Array(4)" :key="item"  />

    </template>
    
    

    <div
      class="py-3 px-3 rounded-md text-base hover:bg-white mb-2"
      v-for="(item, index) in items"
      :key="index"
    >
      <nuxt-link
        class="leading-tight text-gray-700 hover:text-primary-500"
       :to="{ name: 'username-post', params: { username: item.user.username, post: item.id } }"
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
    },
    per_page: {
      type: Number
    }
  },
  data() {
    return {
      items: [],
      loading: false
    }
  },

  methods: {
    async getPostsByTag() {
      this.loading = true

      const res = await this.$axios.get("/articles", {
        params: { tag: this.title, per_page: this.per_page }
      });

      this.items = res.data.map(item => {
        return {
          id: item.id,
          title: item.title,
          new: false,
          comments_count: item.comments_count,
          slug: item.slug,
          user: item.user
        }
      });

      this.loading = false

    }
  }
};
</script>

<style lang="scss" scoped></style>
