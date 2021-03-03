<template>
    <div class="bg-white">
         <div class="md:border border-b md:rounded-md bg-white p-4 hidden md:block">
                    <h2 class="text-lg font-bold">
                        <span class="text-primary-500">DEV Community</span> is a community of 573,072 amazing developers
                    </h2>
                    <p class="mt-4 text-gray-500 leading-tight">We're a place where coders share, stay up-to-date and grow their careers.</p>
                    <button class="block bg-primary-600 py-2 hover:text-primary-600 text-white rounded-md text-center font-semibold w-full mt-2">Create new account</button>
                    <button class="block py-2 text-primary-500 hover:bg-gray-100 rounded-md text-center font-semibold w-full mt-2">Log in</button>
                </div>
                <NavLeft />

                <NavTagLeft />

                
                <div class="my-4 mx-8 lg:mx-0 hidden md:block">
                    <img class="rounded-md" src="@/assets/img/dev-shirt.jpg" alt="">
                    <h3 class="text-lg text-center my-4 text-primary-500 font-bold">DEV Up Your Style</h3>
                </div>

    </div>
</template>

<script>
import NavLeft from './NavLeft.vue'
import NavTagLeft from './NavTagLeft.vue'
    export default {
  components: { NavLeft, NavTagLeft },
       
    }
</script>

<style lang="scss" scoped>

</style>