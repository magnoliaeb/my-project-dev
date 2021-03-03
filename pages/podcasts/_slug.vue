<template>
  <div class="h-screen">
    <!-- podcast -->
    <div class="bg-error-400 w-full py-6 lg:mb-4">
      <div
        class="text-center md:flex md:justify-center md:items-center md:space-x-8"
      >
        <img
          v-if="podcasts[0]"
          class="h-28 w-28 bg-gray-300 rounded-full mb-3 inline-block"
          :src="podcasts[0].image_url"
          alt=""
        />
        <h2 class="text-3xl md:text-4xl mb-3 text-white font-black">
          {{ this.$route.params.slug }}
        </h2>
        <button
          class="bg-primary-500 hover:bg-primary-400 py-2 px-4 text-white font-semibold text-lg rounded-md mx-4"
        >
          Follow
        </button>
      </div>
    </div>
    <div class="lg:flex lg:justify-center">
      <div class="lg:w-6/12">
        <template v-if="$fetchState.pending">
          <SkeletonCardPodcast v-for="(item, index) in Array(5)" :key="index" />
        </template>
        <template v-else>
          <Podcast
            
            :podcast="podcast"
            v-for="(podcast, index) in podcasts"
            :key="index"
          />

          <infinite-loading @infinite="infiniteHandler">
            <div slot="spinner">
              <SkeletonCardPodcast
                v-for="(item, index) in Array(5)"
                :key="index"
              />
            </div>
          </infinite-loading>

        </template>
      </div>
    </div>
  </div>
</template>

<script>
import SkeletonCardPodcast from "../../components/shared/SkeletonCardPodcast.vue";
export default {
  components: { SkeletonCardPodcast },
  data() {
    return {
      podcasts: [],
      page: 1,
      per_page: 5,
      loading: false,
      title: this.$route.params.slug
    };
  },
  head() {
    return {
      title: this.title,
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Home page description"
        }
      ]
    };
  },
  async fetch() {
    await this.getPoscasts();
  },
  methods: {
    async getPoscasts() {
      try {
        const res = await this.$axios.get("/podcast_episodes", {
          params: { username: this.$route.params.slug, per_page: this.per_page }
        });
        this.podcasts = res.data;
        
      } catch (error) {
        console.error(error)
        return false
      }
    },
    async infiniteHandler($state) {
      this.page++;
      const res = await this.$axios.get("/podcast_episodes", {
        params: { username: this.$route.params.slug, page: this.page }
      });

      console.log(res.data.length);
      if (res.data.length > 0) {
        this.podcasts = this.podcasts.concat(res.data);
        $state.loaded();
      } else {
        $state.complete();
      }
    }
  }
};
</script>

<style lang="scss" scoped></style>
