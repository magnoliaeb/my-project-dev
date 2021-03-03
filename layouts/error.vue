<template>
  <div class="h-screen">
    <div v-if="error.statusCode === 404" class=" flex items-center justify-center h-full">
      <img src=".../../../assets/img/undraw_page_not_found_su7k.svg" alt="error" class="h-72">
    </div>
  </div>
</template>

<script>
  export default {
    props: ['error'],
    layout: 'error' // you can set a custom layout for the error page
  }
</script>