<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Ingredients</h1>
    <input
      type="text"
      v-model="keyword"
      class="rounded border-2 border-gray-200 w-full"
      placeholder="Search for Ingredients"
    />
    <router-link
      v-for="ingredient of computedIngredients"
      :key="ingredient.idIngredient"
      :to="{
        name: 'byIngredient',
        params: { ingredient: ingredient.strIngredient },
      }"
    >
      <h3>{{ ingredient.strIngredient }}</h3>
      <pre>{{ ingredient.strDescription }}</pre>
    </router-link>
  </div>
</template>

<script setup>
import { computed, onMounted, ref } from "vue";
import axiosClient from "../axiosClient";

const keyword = ref("");
const ingredients = ref([]);

const computedIngredients = computed(() => {
  if (!computedIngredients) return ingredients;
  return ingredients.value.filter((i) => {
    return (
      (i.strIngredient || "")
        .toLowerCase()
        .includes(keyword.value.toLowerCase())     );
  });
});

onMounted(() => {
  axiosClient.get("list.php?i=list").then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>
