<template>
  <div
    class="my-5 bg-slate-100 dark:bg-slate-800 dark:text-white py-5 px-10 rounded-full relative"
  >
  <header>
    <nav class="flex justify-between pb-10">
      <input
        v-model="fruitName"
        type="text"
        class="bg-gray-200/50 text-gray-800 dark:text-white hover:-translate-y-1 hover:scale-100 hover:bg-gray-200/75 duration-300 text-xl px-5 py-3 rounded-full lg:w-1/4 md:w-1/3 w-1/2 drop-shadow-md"
        placeholder="Strawberry, Banana..."
      />
      <div class="flex flex-row space-x-6">
        <Basket :basket="basket" ref="basket" />
        <ThemeButton />
      </div>
    </nav>
  </header>
    <FruitList
      :fruitName="fruitName"
      :fruits="fruits"
      @addToBasket="addToBasket"
    />
  </div>
</template>

<script>
import fruitData from "../data/fruits.json";
import ThemeButton from "./components/ThemeButton.vue";
import Basket from "./components/Basket.vue";
import FruitList from "./components/FruitList.vue";

export default {
  name: "App",
  data() {
    return {
      basket: [],
      fruits: [],
      fruitName: "",
      selectedFruit: {},
    };
  },
  components: {
    ThemeButton,
    Basket,
    FruitList,
  },
  mounted() {
    this.fruits = fruitData.fruit;
  },
  methods: {
    addToBasket(fruit) {
      this.$refs.basket.addFruitToBasket(fruit);
    },
  },
};
</script>
