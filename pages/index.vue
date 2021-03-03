<template>
  <div>
    <div class="">
      <div class="md:flex pt-4">
        <div class="hidden md:block lg:w-1/4 w-1/3 px-4">
          <!-- <p>left</p> -->
          <SliderLeft />
        </div>

        <div class="md:w-2/3 lg:w-2/4 md:px-4">
          <div class="flex justify-between items-center">
            <h1 class="text-2xl md:text-3xl font-bold p-4">Posts</h1>
            <div class="hidden md:block">
              <Tabs />
            </div>
          </div>

          <template v-if="$fetchState.pending">
            <SkeletonCardPost v-for="(item, index) in Array(4)" :key="index" />
          </template>

          <p v-else-if="$fetchState.error">Error while fetching posts</p>

          <template v-else>

            <Post
              v-for="(post, index) in posts"
              :key="index"
              :post="post"
            />

            <infinite-loading @infinite="infiniteHandler">
              <div slot="spinner">
                <SkeletonCardPost
                  v-for="(item, index) in Array(4)"
                  :key="index"
                />
              </div>
            </infinite-loading>
          </template>
        </div>
        <div class="hidden lg:w-1/4 lg:block px-2">
          <Dev />
          <div>
             <ListListings />
            <ListRight :per_page="5" class="border-b " :title="'news'" />
            <ListRight :per_page="5" :title="'news'" />
            <ListRight :per_page="4" :title="'help'" />
            <ListRight :per_page="3" :title="'discuss'" />
            <ListRight :per_page="2" :title="'explainlikeimfive'" />
            <ListRight :per_page="4" :title="'challenge'" />
            <ListRight :per_page="2" :title="'meta'" />
            <ListRight :per_page="5" :title="'watercooler'" /> 
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Dev from "../components/dev.vue";
import ListListings from "../components/ListListings.vue";
import ListRight from "../components/ListRight.vue";
import SkeletonCardPost from "../components/shared/SkeletonCardPost.vue";
import SliderLeft from "../components/SliderLeft.vue";
export default {
  components: { SkeletonCardPost, SliderLeft, ListRight, ListListings, Dev },

  data() {
    return {
      posts: [],
      page: 1,
      per_page: 4,
      items: [],
      title: "Home"
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
    await this.getPosts()
   
  },

  methods: {
    async getPosts() {
      try {
        const res = await this.$axios.get("/articles", {
       params: { per_page: this.per_page, state: 'rising', tag: 'vue' }
     });
     this.posts = res.data.map((item, i) => {
       if (i === 0) {
         return {
           ...item
         };
       } else {
         delete item.social_image;
         return {
           ...item
         };
       }
     });
        
      } catch (error) {
        console.error(error)
        return false
      }

    },
    async infiniteHandler($state) {
      this.page++;
      const res = await this.$axios.get("/articles", {
       params: { per_page: this.per_page, state: 'rising', tag: 'vue' }
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
    }
  }
};
</script>
