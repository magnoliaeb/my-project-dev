<template>
  <div class="space-x-1.5">
    <div @click="$router.push('/')"
      class="px-2 hover:bg-primary-500 hover:bg-opacity-10 hover:text-primary-500 rounded-md py-2 text-center focus:outline-none inline-block"
      
    >
      <span>
        <router-link to="/" active-class="text-primary-500 border-b-2 border-primary-500" exact>Feed</router-link>
      </span>
    </div>
    <div @click="$router.push({ name: 'top-top', params: { top: tab.to}})"
      class="px-2 hover:bg-primary-500 hover:bg-opacity-10 hover:text-primary-500 rounded-md py-2 text-center focus:outline-none inline-block"
      v-for="(tab, index) in tabs"
      :key="index"
      
    >
      <span>
        <router-link :to="{ name: 'top-top', params: { top: tab.to}}" active-class="text-primary-500 border-b-2 border-primary-500" exact>{{ tab.title }} </router-link>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  
  data() {
    return {
      tabs: [
        { title: "Yesterday", to: 'yesterday'},
        { title: "Week", to: 'week'},
        { title: "Month", to: 'month' },
        { title: "Year", to: 'year' }
      ]
    }
  },
  
 
};
</script>

<style scoped>
</style>
