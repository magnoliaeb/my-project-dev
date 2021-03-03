<template>
  <div>
    <template v-if="$fetchState.pending">
      <SkeletonCardListing v-for="(item, index) in Array(3)" :key="item" />
    </template>

        <p v-else-if="$fetchState.error">Error while fetching listings</p>
        <template v-else>
        <listing
          v-for="(listing, index) in listings"
          :key="index"
          :listing="listing"
        />

        <infinite-loading @infinite="infiniteHandler">
          <div slot="spinner">
            <SkeletonCardListing v-for="(item, index) in Array(3)" :key="index" />
          </div>
        </infinite-loading>

        </template>
  </div>
</template>

<script>
import NavListingLeft from "@/components/NavListingLeft.vue";
import SkeletonCardListing from "@/components/shared/SkeletonCardListing.vue";
export default {
  components: { SkeletonCardListing, NavListingLeft },
  data() {
    return {
      listings: [],
      page: 1,
      per_page: 3,
      loading: true,
    };
  },

  async fetch() {
    await this.getListings();
  },
  watch: {
    // call again the method if the route changes
    $route: "getListings"
  },

  methods: {
    async getListings() {
      try {
        const res = await this.$axios.get("/listings", {
          params: { per_page: this.per_page }
        });
  
        this.listings = res.data;
        
      } catch (error) {
        console.error(error)
        return false
      }

    },
    async infiniteHandler($state) {
      this.page++;
      const res = await this.$axios.get("/listings", {
        params: { page: this.page }
      });
      if (res.data.length > 0) {
        this.listings = this.listings.concat(res.data);
        $state.loaded();
      } else {
        $state.complete();
      }
    }
  }
};
</script>
