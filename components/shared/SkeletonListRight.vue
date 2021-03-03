<template>
     <div class="">
        <header class="px-3 py-2">
            <h2 class="bg-gray-300 h-4 w-32 rounded-md animate-pulse"></h2>
        </header>
        <div class="py-3 px-3 mb-2" v-for="(item, index) in Array(6)" :key="index">
            
                 <p class="bg-gray-300 rounded-md h-4 w-full mb-2 animate-pulse"></p>
            <p  class="bg-gray-300 rounded-md h-3 w-28 animate-pulse"></p>
        </div>
    </div>
</template>
