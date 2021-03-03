<template>
  <div class="bg-gray-50">
    <div
      class="px-6 py-4 bg-white shadow border-t-4 md:border-t-8 border-pink-600 lg:mx-28"
    >
      <div class="flex justify-between">
        <h2 class="text-2xl font-bold md:text-3xl">{{ tagSelected }}</h2>
        <div>
          <button
            class="text-primary-500 font-semibold hover:bg-primary-500 hover:bg-opacity-10 hover:text-primary-500 rounded-md py-2 text-center px-4 focus:outline-none"
          >
            Follow
          </button>
              <button
              class="text-gray-500 font-semibold hover:bg-gray-500 hover:bg-opacity-10 hover:text-gray-500 rounded-md py-2 text-center px-4 focus:outline-none"
              >
              Discard
              </button>

        </div>
      </div>
    </div>
    <div class="md:flex pt-4">
      <div class="hidden md:block lg:w-1/4 w-1/3 px-4 lg:px-8">
        <!-- <p>left</p> -->
        <div class="space-y-4 divide-y divide-gray-200">
          <div>
            <h2 class="font-mono font-semibold my-4">submission guidelines</h2>
            <p class="leading-tight text-gray-800 mb-3">
              Be nice. <br />
              Be respectful. <br />
              Assume best intentions. <br />
              Be kind, rewind.
            </p>
            <button
              class="px-4 py-2 text-sm bg-primary-500 text-white rounded-md focus:outline-none hover:bg-primary-600"
            >
              Write a post
            </button>
          </div>
          <div class="">
            <h2 class="font-mono font-semibold my-4">tag moderators</h2>
            <div class="flex -space-x-2">
              <img
                class="w-14 h-14 border-2 border-white object-cover rounded-full"
                src="../../assets/img/moderators/moderators-1.jpg"
                alt=""
              />
              <img
                class="w-14 h-14 border-2 border-white object-cover rounded-full"
                src="../../assets/img/moderators/moderators-2.png"
                alt=""
              />
              <img
                class="w-14 h-14 border-2 border-white object-cover rounded-full"
                src="../../assets/img/moderators/moderators-3.gif"
                alt=""
              />
              <img
                class="w-14 h-14 border-2 border-white object-cover rounded-full"
                src="../../assets/img/moderators/moderators-4.jpg"
                alt=""
              />
            </div>
          </div>
          <div class="text-gray-700 font-mono py-4 font-semibold">
            <p>{{ totalPost }} Posts Published</p>
          </div>
        </div>
      </div>

      <div class="md:w-2/3 lg:w-2/4 md:px-4">
        <!-- login -->
        <div v-if="this.posts.length > 0"
          class="p-4 rounded-md mx-2 mb-4 md:mx-0 text-lg bg-primary-500 text-primary-500 bg-opacity-10"
        >
          <h3>
            <nuxt-link to="" class="text-xl font-semibold">Sign in</nuxt-link>
            for the ability sort posts by top and latest.
          </h3>
        </div>

        <template v-if="$fetchState.pending">
         
          <SkeletonCardPost  v-for="(item, index) in Array(4)" :key="index"/>
        </template>

        <p v-else-if="$fetchState.error">Error while fetching posts</p>
        <template v-else>
            
        <Post v-for="(post, index) in posts" :key="index" :post="post" />

        <infinite-loading @infinite="infiniteHandler">
          <div slot="spinner">
                <SharedSkeletonCardPost
                
                v-for="(item, index) in Array(4)"
                :key="index"
                />
            </div>
        </infinite-loading>
        </template>


      </div>

      <div class="hidden lg:w-1/4 lg:block px-2">
      
        <ListRight :title="'dicuss'" />
      
      </div>
    </div>
  </div>
</template>

<script>
import ListRight from "../../components/ListRight.vue";
import Post from "../../components/Post.vue";
import SkeletonCardPost from '../../components/shared/SkeletonCardPost.vue';
import SkeletonListRight from '../../components/shared/SkeletonListRight.vue';
export default {
  components: { Post, ListRight, SkeletonCardPost, SkeletonListRight },
  computed: {
    totalPost() {
      return Math.floor(Math.random() * 20000) + 200;
    }
  },
  data() {
    return {
      tagSelected: this.$route.params.tag,
      posts: [],
      page: 1,
      per_page: 4,
      items: [],
      loading: true,
      title: this.$route.params.tag
    };
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

  async fetch() {
    await this.getPostByTag()
    
    
    
    },
  methods: {
    async getPostByTag() {
      try {
        const res = await this.$axios.get("/articles", {
            params: { tag: this.tagSelected, per_page: this.per_page }
          });
          this.posts = res.data.map((item, i) => {
            delete item.social_image;
            return {
              ...item
            };
          });
        
      } catch (error) {
        console.error(error)
        return false
      }
      
    },
   
    async infiniteHandler($state) {
      this.page++;
      const res = await this.$axios.get("/articles", {
        params: { tag: this.tagSelected, page: this.page }
      });

      if (res.data.length > 0) {
        this.posts = this.posts.concat(
            res.data.map((item, i) => {
            delete item.social_image;
            return {
              ...item
            };
        })
        );
        $state.loaded();
      } else {
        $state.complete();
      }
    },
   
  }
};
</script>

<style scoped>
.router-link-active {
  font-weight: bold;
}
</style>
