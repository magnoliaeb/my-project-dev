<template>
    <div class="border-r">
        <h3 class="font-medium text-gray-900 my-4">podcasts</h3>
                    <ul class="space-y-1 ">
                       

                               <li  class="flex hover:bg-gray-200 py-1 px-3 rounded" v-for="(podcast, index) in podcasts" :key="index">
                                <img class="w-8 h-8 bg-primary-500 rounded-full flex-none mr-2" :src="podcast.podcast.image_url" alt="">
                                <h4 class="font-bold text-sm">
                                    <nuxt-link :to="{ name: 'podcasts-slug', params: { slug: podcast.podcast.slug } }">
                                    
                                        {{ podcast.podcast.title }}
                                    </nuxt-link>
                                    </h4>
                            </li>
                    </ul>
                    <span class="pt-5 text-gray-600 block">Suggest a Podcast</span>

    </div>
</template>

<script>
import SkeletonItemPodcastLeft from './shared/SkeletonItemPodcastLeft.vue';
    export default {
  components: { SkeletonItemPodcastLeft },
        data() {
            return {
                podcasts: [],
            }
        },
        async mounted () {
            await  this.getPodcasts();
        },
        methods: {
             async getPodcasts() {
                const res = await this.$axios.get('/podcast_episodes')
                this.podcasts = res.data
                
            },
        },
    }
</script>
