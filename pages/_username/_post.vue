<template>
    <div class="" v-if="post">
        <div class="flex flex-col lg:flex-row justify-between lg:mt-4">
            <div class="w-32 bg-error-300 hidden md:block">
                left
                <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime eaque illo culpa rem, eius, nulla perspiciatis aperiam sequi dignissimos aliquid nemo officia deserunt soluta. Ratione debitis velit aspernatur ex necessitatibus!</p>
            </div>



            <div class="lg:w-3/5 w-full mb-10 ">
                <div class="bg-white border">
                    <article >
                        <img class="h-52 lg:h-72 bg-gray-500 w-full object-cover" :src="post.social_image" alt="">
                        <div class="px-6 py-8">
                            <h1 class="md:text-5xl text-2xl font-bold tracking-wide leading-tight mb-2">{{ post.title }}</h1>
                            <div class="mt-2 text-gray-600">
                                
                                <ul class="flex space-x-1 mt-2">
                                    <li v-for="(tag, index) in post.tags" :key="index" class="px-1 rounded-md">
                                        <router-link :to="{ name: 'tags-tag', params: { tag: tag }}">#{{ tag }}</router-link>
                                        </li>
                               
                                </ul>
                                <div v-if="post.user" class="mt-4 flex items-center">
                                    <img  :src="post.user.profile_image" alt="" class="w-10 h-10 bg-gray-300 rounded-full mr-3">
                                    <p class="text-gray-800">{{ post.user.name }}</p>
                                </div>
                                <div class="my-4">
                                    <p class="text-gray-500 text-sm">{{ post.readable_publish_date }} <span class="italic">Originally published at <a :href="post.path" target="_blank" class="text-primary-400">{{ post.canonical_url}}</a> </span>・3 min read</p>
                                </div>
                                

                            </div>
                            <div class="" v-html="post.body_html"></div>
                            
                        </div>
                    </article>
                </div>
                <div class="p-4 bg-white shadow mt-4">
                    <div class="flex justify-between items-center">
                        <h3 class="text-xl font-bold">Discussion (6)</h3>
                                <button class="px-4 py-2 bg-white rounded-md border">Subscribe</button>
                    </div>
                    <div class="flex mt-4">
                        <img src="" alt="" class="w-6 h-6 rounded-full flex-none mr-3">
                        <textarea class="border w-full rounded-md p-2 placeholder-gray-500 resize-none" name="comment" id="comment" rows="3">Add to the discussion</textarea>
                    </div>
                    <div>
                    <div class="flex mt-4">
                        <img src="" alt="" class="w-6 h-6 rounded-full bg-error-400 flex-none mr-3">
                        <div class="border w-full rounded-md p-3 placeholder-gray-500 resize-none">
                            <div>
                                <span class="text-sm font-semibold text-gray-500">WebsiteMarket • Feb 22</span>
                            </div>
                            <p class="mt-3">MIT License?</p>
                        </div>
                    </div>
                        <div class="pl-14 mt-2">
                            <button>3</button>
                            <button>3</button>
                        </div>

                    </div>
                    <p class="mt-2 text-center text-sm text-gray-500">Code of Conduct • Report abuse</p>
                </div>


                <div class="py-6 bg-white px-4 mt-4 border lg:p-10">
                    <h3 class="text-xl font-bold mb-4 md:text-2xl">Read next</h3>
                    <ul class="space-y-6">
                        
                        <li class="flex items-center" v-for="(post, index) in nextPost" :key="index">
                            <img :src="post.social_image" alt="" class="lg:w-16 lg:h-16 w-12 h-12 rounded-full mr-3 flex-none">
                        <div class="leading-tight">
                                <h4 class="text-lg font-bold m-0 hover:text-primary-500 md:text-2xl">
                                    <router-link :to="{ name: 'username-post', params: { username: post.user.username, post: post.id } }">{{ post.title }}</router-link>
                                </h4>
                            <p v-if="post.user" class="text-gray-500 font-semibold m-0 hover:text-primary-400">{{ post.user.name }} - {{ post.readable_publish_date}}</p>
                        </div>
                        </li>
                    </ul>

                </div>

            </div>

            <div class="lg:w-1/4 w-full lg:mx-2">
                <div class="shadow bg-white">
                    <div class="relative mb-8">
                        <div class="h-10 bg-primary-300 rounded-t-md">

                        </div>
                        <div v-if="post.user" class="flex items-end absolute top-3 left-4">
                            <img :src="post.user.profile_image" alt="" class="h-12 w-12 object-cover rounded-full mr-3">
                            <h2 class="font-bold text-lg">{{ post.user.name }}</h2>
                        </div>

                    </div>
                    <div class="p-4 text-gray-800">
                    <!-- <p>Premium and free Bootstrap 4 Themes and UI Kits</p> -->
                    <button class="block bg-primary-600 py-2 text-white rounded-md text-center font-semibold w-full my-4">Follow</button>
                    <!-- <p>Get premium and free Bootstrap 4 Themes!</p> -->
                    <!-- <button class="block bg-white text-gray-500 rounded-md py-2 text-center font-semibold w-full my-4 border ">Themesberg</button> -->


                    </div>
                </div>
                <div class="mt-4 mb-8 bg-white border shadow">
                    <h3 v-if="post.user" class="text-lg font-bold border-b p-4">More from <span class="text-primary-500">{{ post.user.name }}</span></h3>
                    
                    <div class="space-y-4 border-b py-4" v-for="(item, index) in posts" :key="index">
                       <div class="px-4">
                            <p class="text-gray-800">
                                <router-link  :to="{ name: 'username-post', params: { username: item.user.username, post: item.id } }">

                                {{ item.title }}
                                </router-link> </p>
                        <ul class="text-gray-500 flex text-sm mt-2  space-x-2">
                            
                            <li v-for="(tag, index) in item.tag_list" :key="index">

                                <p>
                                <router-link :to="{ name: 'tags-tag', params: { tag: tag }}">
                                    #{{ tag }}
                                </router-link>
                                </p>
                            </li>
                            
                        </ul>
                       </div>

                    </div>
                </div>
            </div>

        </div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
                post: {},
                title: null,
                posts: [],
                nextPost: []

            }
        },
         head() {
            return {
                title: this.title,
                meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: 'Home page description'
                }
                ]
            }
        },
     '$route.query': '$fetch',

        async fetch() {
            await this.getPosById()
            // this.title = this.post.title
            },

        async mounted () {
            await this.getPostByUser()
            await this.getNextPostByUser()
            
        },
         
        methods: {
          async getPosById() {
              try {
                  
                  const res = await this.$axios.get(`/articles/${this.$route.params.post}`)
                  this.post = res.data
              } catch (error) {
                  console.error(error)
        return false
              }

            },
          async getPostByUser() {
              try {
                  const res = await this.$axios.get(`/articles`,
                         {params: { per_page: 4, state: 'rising', username: this.$route.params.username } }
  
                  )
                  this.posts = res.data
                  
              } catch (error) {
                  console.error(error)
        return false
              }

            },
          async getNextPostByUser() {
              try {
                  const res = await this.$axios.get(`/articles`,
                         {params: { per_page: 4, state: 'rising', tag: 'vue', page: 2 } }
  
                  )
                  this.nextPost = res.data
                  
              } catch (error) {
                  console.error(error)
        return false
              }

            },
             
        },
    }
</script>
