<template>
    <div class="h-screen">
        <div class="lg:p-6">
            <h1 class="text-gray-900 text-center text-3xl font-bold py-4">DEV Community on Video</h1>

            <div class="flex flex-col md:flex-row md:flex-wrap">
                
                <template v-if="loading">
                    <SkeletonCardVideo v-for="(item, index) in Array(3)" :key="index" />  
                </template>
                

                <Video v-else v-for="(video, index) in videos" :key="index" :video="video" />

                <infinite-loading @infinite="infiniteHandler">
                    <div slot="spinner">
                        <div class="flex flex-col md:flex-row md:flex-wrap">
                        <SkeletonCardVideo v-for="(item, index) in Array(3)" :key="index" />  

                        </div>
                    </div>
                </infinite-loading> 

            </div>


            

        </div>

    </div>
</template>

<script>
import SkeletonCardVideo from '../components/shared/SkeletonCardVideo.vue'


    export default {
  components: { SkeletonCardVideo },
        data() {
            return {
                videos: [],
                page: 1,
                per_page: 3,
                loading: false,
                title: 'Videos'
            }
        },
         head() {
            return {
                title: this.title,
                meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Videos page description'
                }
                ]
            }
        },

        async fetch() {
            await this.getVideos()
        },

        methods: {
            async getVideos() {
                this.loading = true
                const res = await this.$axios.get('/videos', { params: { per_page: this.per_page }})
                this.videos = res.data
                this.loading = false
                
            },
            async infiniteHandler($state) {
                this.page++
                this.loading = true
                // const res = await this.$axios.get('/videos', { params: { page: this.page }})
                // if (res.data) {
                    
                //     console.log(this.page)
                //     this.videos = this.videos.concat(res.data);
                //     $state.loaded();
                // } else {
                //     $state.complete();
                // }


                
            }
        },
    }

</script>

<style lang="scss" scoped>

</style>