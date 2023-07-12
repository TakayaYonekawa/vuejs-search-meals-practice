<template>
  <div class="p-8">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Ingredients</h1>
    <router-link
      v-for="ingredient of ingredients"
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
import { onMounted, ref } from "vue";
import axiosClient from "../axiosClient";

const ingredients = ref([]);

onMounted(() => {
  axiosClient.get("list.php?i=list").then(({ data }) => {
    ingredients.value = data.meals;
  });
});
</script>
