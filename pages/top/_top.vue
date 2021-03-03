
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
      <Post  v-for="(post, index) in posts" :key="index" :post="post" />

      <infinite-loading @infinite="infiniteHandler">
        <div slot="spinner">
          <SkeletonCardPost v-for="(item, index) in Array(4)" :key="index" />
        </div>
      </infinite-loading>
      
    </template>

      </div>
      <div class="hidden lg:w-1/4 lg:block px-2">
        <div >
        <ListRight class="border-b " :title="'news'" />
               <ListRight :title="'news'" />
               <ListRight :title="'help'" />
               <ListRight :title="'discuss'" />
               <ListRight :title="'explainlikeimfive'" />
               <ListRight :title="'challenge'" />
               <ListRight :title="'meta'" />
               <ListRight :title="'watercooler'" />

        </div>
      </div>
    </div>
  </div>

    
  </div>
</template>

<script>
import SkeletonCardPost from '../../components/shared/SkeletonCardPost.vue';
export default {
  components: { SkeletonCardPost },
  data() {
    return {
      posts: [],
      page: 1,
      per_page: 4,
      loading: true,
      items: [],
     
    };
  },
  

  async fetch() {
    await this.getPostsByTop();
  },
  watch: {
    // call again the method if the route changes
    '$route': 'getPostsByTop'
  },

    head() {
        return {
            title: `Top post this ${this.$route.params.top}`,
            meta: [
            {
                hid: 'description',
                name: 'description',
                content: 'Home page description'
            }
            ]
        }
    },


  methods: {
    async getPostsByTop() {

      try {
        const res = await this.$axios.get("/articles", {
          params: { per_page: this.per_page, top: this.getTop(), state: 'rising', tag: 'vue' }
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
    getTop() {
      let top = null;
      switch (this.$route.params.top) {
          case 'yesterday':
              top = 1;
              
              break;
          case 'week':
              top = 7;
              
              break;
          case 'month':
              top = 30;
              
              break;
      
          default:
              top = 365;
              break;
      }
      return top
    },
    async infiniteHandler($state) {
      this.page++;
      const res = await this.$axios.get("/articles", {
        params: { per_page: this.per_page, top: this.getTop(), state: 'rising', tag: 'vue' }
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

