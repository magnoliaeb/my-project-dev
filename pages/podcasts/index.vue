<template>
  <div class="h-screen">
    <div class="lg:flex">
      <!-- navegacion left -->
      <div class="w-3/12 hidden lg:block px-4">
        <NavPodcastLeft />
      </div>

      <!-- podcast -->
      <div class="lg:w-9/12 lg:flex lg:justify-center">
        <div class="lg:w-8/12 mt-4">
          <template v-if="$fetchState.pending">
            <SkeletonCardPodcast
              v-for="(item, index) in Array(5)"
              :key="index"
            />
          </template>

          <p v-else-if="$fetchState.error">Error while fetching podtcasts</p>

          <Podcast
            v-else
            :podcast="podcast"
            v-for="(podcast, index) in podcasts"
            :key="index"
          />

          <!-- teams -->
          <nuxt-link to="/" class="lg:mt-3">
            <template v-if="$fetchState.pending">
              <SkeletonPodcast v-for="(item, index) in Array(5)" :key="index" />
            </template>
            

            <template v-else>
              <article
                v-if="podcast.podcast"
                v-for="(podcast, index) in podcasts"
                :key="index"
                class="flex p-4 border-b bg-white mb-3 ld:rounded ld:shadow"
              >
                <img
                  class="w-10 h-10 bg-error-500 rounded-xl flex-none mr-2"
                  :src="podcast.podcast.image_url"
                  alt=""
                />
                <div>
                  <p
                    class="text-gray-500 font-semibold text-sm hover:underline"
                  >
                    {{ podcast.podcast.title }}
                  </p>
                  <h2 class="text-xl font-bold leading-tight">
                    {{ podcast.podcast.title }}
                  </h2>
                </div>
              </article>
            </template>
          </nuxt-link>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import NavPodcastLeft from "../../components/NavPodcastLeft.vue";
import SkeletonCardPodcast from "../../components/shared/SkeletonCardPodcast.vue";
import SkeletonPodcast from "../../components/shared/SkeletonPodcast.vue";
export default {
  components: { SkeletonCardPodcast, NavPodcastLeft, SkeletonPodcast },
  data() {
    return {
      podcasts: [],
      loading: false
    };
  },
  head() {
    return {
      title: "Podcasts",
      meta: [
        {
          hid: "description",
          name: "description",
          content: "Podcasts page description"
        }
      ]
    };
  },
  async fetch() {
    await this.getPodcasts();
  },
  methods: {
    async getPodcasts() {
      try {
        const res = await this.$axios.get("/podcast_episodes");
        this.podcasts = res.data;
        
      } catch (error) {
        console.error(error)
        return false
      }
    }
  }
};
</script>
