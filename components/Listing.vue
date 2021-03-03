<template>
    <article  class="bg-white shadow mb-2">
                    <div class="px-2 py-4">
                        
                        <div class="md:pl-10">
                            <h2 class="text-xl md:text-3xl mt-4 font-bold hover:text-primary-500">
                                {{ listing.title }}
                            </h2>
                        <ul class="flex mt-2">
                            <li class="mr-2 text-sm flex-none text-gray-500 hover:text-gray-900" 
                            v-for="(tag, index) in listing.tags" :key="index"
                            
                            >
                                #{{ tag }}
                            </li>
                        </ul>
                        <div v-html="listing.processed_html"></div>
                        <div class="flex items-center mt-4">
                  
                        <img class="w-8 h-8 bg-gray-500 rounded-full mr-2 flex-none" :src="listing.user.profile_image" alt="">
                            <div>
                                <h3 class="text-gray-600 font-semibold text-sm">{{ listing.user.name }}</h3>
                            </div>
                        </div>
                        
                        </div>
                    </div>
                </article>
</template>

<script>
    export default {
        props: {
            listing: {
                type: Object,
            },
        },
       
    }
</script>

<style lang="scss" scoped>

</style>