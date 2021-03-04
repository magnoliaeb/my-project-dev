<template>
    <div class="h-screen">
        <div class="lg:p-6">
            <h1 class="text-gray-900 text-left text-3xl font-bold py-4">Top tags</h1>

            <div class="flex flex-col md:flex-row md:flex-wrap">
                <template  v-if="$fetchState.pending">
                    <skeleton-tag v-for="(item, index) in Array(18)" :key="index" />  
                        
                </template>
                    <p v-else-if="$fetchState.error">Error while fetching tags</p>



                <template v-else>
                    <Tag v-for="(tag, index) in tags" :tag="tag" :key="index"/>

                    <infinite-loading @infinite="infiniteHandler">
                        <div slot="spinner">
                            <div class="flex flex-col md:flex-row md:flex-wrap">
                            <skeleton-tag v-for="(item, index) in Array(18)" :key="index" />  

                            </div>
                        </div>
                    </infinite-loading>

                </template>
               

            </div>


            

        </div>

    </div>
</template>

<script>
import SkeletonTag from '../../components/shared/SkeletonTag.vue'


    export default {
  components: { SkeletonTag },
        data() {
            return {
                tags: [],
                page: 1,
                per_page: 18,
                loading: false,
                title: 'Top tags',
                loading: true
            }
        },
        
        head() {
            return {
                title: this.title,
                meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Tags page description'
                }
                ]
            }
        },

        async fetch() {
            await this.getTags()
        },

        methods: {
            async getTags() {
                try {
                    const res = await this.$axios.get('/tags', { params: { per_page: this.per_page, page: this.page  }})
                    this.tags = res.data
                    
                } catch (error) {
                    console.error(error)
        return false
                }
                
            },
            async infiniteHandler($state) {
                this.page++
                const res = await this.$axios.get('/tags', { params: { page: this.page }})
                if (res.data) {
                    
                    console.log(this.page)
                    this.tags = this.tags.concat(res.data);
                    $state.loaded();
                } else {
                    $state.complete();
                }


                
            }
        },
    }

</script>