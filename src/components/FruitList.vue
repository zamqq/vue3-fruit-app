<template>
  <div
    class="bg-slate-100 dark:bg-slate-800 dark:text-white py-5 px-10 rounded-full relative"
  >
    <div class="flex justify-between pb-10">
      <input
        @keypress="getFruits"
        v-model="fruitName"
        type="text"
        class="bg-gray-200/50 text-gray-800 dark:text-white hover:-translate-y-1 hover:scale-100 hover:bg-gray-200/75 duration-300 text-xl px-5 py-3 rounded-full lg:w-1/4 md:w-1/3 w-1/2 drop-shadow-md"
        placeholder="Strawberry, Banan..."
      />
      <div class="flex flex-row space-x-6">
        <Basket :basket="basket" ref="basket" />
        <ThemeButton />
      </div>
    </div>
    <div
      class="grid justify-around gap-10 lg:grid-cols-4 md:grid-cols-3 grid-cols-2"
    >
      <NutritionLabel :selected="selectedFruit" />
      <div
        v-for="fruit in filteredFruits"
        :key="fruit.id"
        @click="getInfo(fruit)"
        class="bg-green-300 dark:text-white hover:-translate-y-1 hover:scale-100 duration-300 hover:bg-green-200 rounded-lg drop-shadow-lg relative flex justify-center items-center h-48"
      >
        <p class="text-8xl">{{ fruit.img }}</p>
        <button
          @click="$refs.basket.addFruitToBasket(fruit)"
          class="text-gray-800 border-gray-800 border px-2 rounded-lg absolute bottom-5 right-5 hover:bg-green-200 duration-150 font-medium"
        >
          +
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import fruitData from "../../data/fruits.json";
import NutritionLabel from "./NutritionLabel.vue";
import ThemeButton from "./ThemeButton.vue";
import Basket from "./Basket.vue";

export default {
  name: "FruitList",
  data() {
    return {
      basket: [],
      fruits: [],
      fruitName: "",
      selectedFruit: {},
    };
  },
  components: {
    NutritionLabel,
    ThemeButton,
    Basket,
  },
  mounted() {
    this.fruits = fruitData.fruit;
  },
  methods: {
    getInfo(fruit) {
      this.selectedFruit = this.fruits.filter((item) => {
        return item.name === fruit.name;
      })[0];
    },
  },
  computed: {
    filteredFruits() {
      return this.fruits.filter((fruit) =>
        fruit.name.toLowerCase().includes(this.fruitName.toLowerCase())
      );
    },
  },
};
</script>
