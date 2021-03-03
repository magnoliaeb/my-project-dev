<template>
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

        <router-view></router-view>
      </div>
      <div class="hidden lg:w-1/4 lg:block px-2">
        <div >
        <ListRight class="border-b " :title="'news'" />
               <ListRight class="border-b " :title="'help'" />
               <ListRight class="border-b " :title="'discuss'" />
               <ListRight class="border-b " :title="'challenge'" />
               <ListRight class="border-b " :title="'meta'" />
               <ListRight class="border-b " :title="'watercooler'" />

        </div>
      </div>
    </div>
  </div>
</template>
