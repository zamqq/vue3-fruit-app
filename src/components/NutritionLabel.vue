<template>
  <div
    id="infopack"
    class="bg-transparent text-justify rounded-lg drop-shadow-lg col-span-2 row-span-2 border border-gray-800 dark:border-white"
  >
    <ul class="sm:text-3xl text-2xl sm:my-10 my-5 mx-6" v-if="selected.name">
      <li class="sm:text-4xl text-2xl pb-3">
        Name:<a class="bg-green-300 rounded-full px-4 text-white float-right"
          >{{ selected.name }}
        </a>
      </li>
      <li
        class="sm:text-4xl text-xl mb-7 pb-2 border-b border-gray-800 dark:border-white"
      >
        Nutrition Facts<span class="float-right">per 100g</span>
      </li>
      <li class="pb-1">
        Calories:
        <span class="float-right">{{ selected.nutritions.calories }}</span>
      </li>
      <li class="pb-1">
        Carbohydrate:<span class="float-right"
          >{{ selected.nutritions.carbohydrates }}g</span
        >
      </li>
      <li class="pb-1">
        Protein:<span class="float-right"
          >{{ selected.nutritions.protein }}g</span
        >
      </li>
      <li class="pb-1">
        Fat:<span class="float-right">{{ selected.nutritions.fat }}g</span>
      </li>
      <li>
        Fructose:<span class="float-right"
          >{{ selected.nutritions.sugar }}g</span
        >
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "NutritionLabel",
  props: {
    selected: Object,
  },
};
</script>
