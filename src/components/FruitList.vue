<template>
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
        @click="$emit('addToBasket', fruit)"
        class="text-gray-800 border-gray-800 border px-2 rounded-lg absolute bottom-5 right-5 hover:bg-blue-300 duration-150 font-medium"
      >
        +
      </button>
    </div>
  </div>
</template>

<script>
import NutritionLabel from "./NutritionLabel.vue";

export default {
  name: "FruitList",
  data() {
    return {
      basket: [],
      selectedFruit: {},
    };
  },
  props: {
    fruits: {
      type: Array,
      required: true,
    },
    fruitName: {
      type: String,
      default: "",
    },
  },
  components: {
    NutritionLabel,
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
