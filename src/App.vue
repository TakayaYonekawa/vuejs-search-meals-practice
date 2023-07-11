<template>
  <div class="bg-gray-100 h-full">
    <header class="bg-white shadow h16 flex justify-between items-stretch">
      <router-link :to="{name: 'home' , params: '/home'}" class="inline-flex items-center h-full px-5">
        Home
      </router-link>

      <div class="flex items-center gap-1">
        <router-link to="/" class="inline-flex items-center transition-colors px-2 h-full hover:bg-purple-200">
          Search Meals
        </router-link>
        <router-link to="/" class="inline-flex items-center transition-colors px-2 h-full hover:bg-purple-200">
          Meals By letter
        </router-link>
        <router-link to="/" class="inline-flex items-center transition-colors px-2 h-full hover:bg-purple-200">
          Search By Ingredients
        </router-link>
      </div>
    </header>
    <main>
      <router-view></router-view>
    </main>
  </div>
</template>

<script setup>

</script>