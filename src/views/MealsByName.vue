<template>
  <div class="p-8">
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 border-gray-200 w-full"
      placeholder="Search for Meals"
      @change="searchMeals"
    />
  </div>

  <div>
    <div
      v-for="meal of meals"
      :key="meal.idMeal"
      class="grid grid-cols-1 md:grid-cols-3 gap-5 px-8"
    >
    <router-link :to="{name: 'mealDetails', params: {id: meal.idMeal}}">
      <img
        :src="meal.strMealThumb"
        :alt="strMeal"
        class="rounded-t-xl w-full h-48 object-cover"
      />
    </router-link>
      <h3 class="font-bold">{{ meal.strMeal }}</h3>
      <div class="flex justify-between items-center">
        <a
          :href="meal.strYoutube"
          target="_blank"
          class="px-3 py-2 rounded border-2 text-white border-orange-600 bg-orange-500 hover:bg-orange-600 transition-colors"
          >Youtube</a
        >
        <router-link
          to="/"
          class="px-3 py-2 rounded border-2 text-white border-orange-600 bg-orange-500 hover:bg-orange-600 transition-colors"
          >View</router-link
        >
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from "@vue/reactivity";
import { onMounted, ref } from "vue";
import store from "../store";
import { useRoute } from "vue-router";
const route = useRoute();
const keyword = ref("");
const meals = computed(() => store.state.searchedMeals);

function searchMeals() {
  store.dispatch("searchMeals", keyword.value);
}

onMounted(() => {
  keyword.value = route.params.name
  if(keyword.value){
    searchMeals()
  }
})
</script>
