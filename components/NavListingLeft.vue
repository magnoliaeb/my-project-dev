<template>
  <div>
    <h3 class="font-medium text-gray-900 my-4">Listings</h3>
    <ul class="space-y-1 ">
      <li
        class="flex hover:bg-gray-200 hover:text-primary-500 py-2 px-3 rounded"
      >
        <h4 class="font-bold text-sm">
          <router-link
            :to="{ name: 'listings' }"
            active-class="text-primary-500 py-2 px-3 border-b-2 border-primary-500"
            exact
          >
            All listings
          </router-link>
        </h4>
      </li>

      <li
        v-for="(item, index) in items"
        :item="item"
        :key="index"
        class="flex hover:bg-gray-200 hover:text-primary-500 py-2 px-3 rounded "
      >
        <h4 class="font-bold text-sm">
          <router-link
            active-class="text-primary-500 py-2 px-3 border-b-2 border-primary-500"
            :to="{
              name: 'listings-category',
              params: { category: item.category }
            }"
          >
            {{ item.title }}
          </router-link>
        </h4>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { category: "collabs", title: "Contributors/Collaborators Wanted" },
        { category: "cfp", title: "Conference CFP" },
        { category: "forhire", title: "Available for Hire" },
        { category: "education", title: "Education/Courses" },
        { category: "jobs", title: "Job Listings" },
        { category: "mentors", title: "Offering Mentorship" },
        { category: "mentees", title: "Seeking a Mentor" },
        { category: "forsale", title: "Stuff for Sale" },
        { category: "events", title: "Upcoming Events" },
        { category: "misc", title: "Miscellaneous" },
        { category: "products", title: "Products/Tools" }
      ],
      loading: false
    };
  }
};
</script>
