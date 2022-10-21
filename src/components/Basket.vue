<template>
  <div
    class="relative inline-block text-left"
    @mouseenter="isBasketOpen = true"
    @mouseleave="isBasketOpen = false"
  >
    <div
      class="hover:-translate-y-0.5 hover:scale-100 hover:brightness-95 delay-50 duration-300 drop-shadow-md"
    >
      <button
        type="button"
        class="inline-flex w-full justify-center bg-clip-text hover:-translate-y-1 hover:scale-100 duration-300 text-5xl"
        id="menu-button"
        aria-expanded="true"
        aria-haspopup="true"
        @click="!isBasketOpen"
      >
        🧺
      </button>
      <div class="bg-blue-300">
        <span
          class="float-right font-normal px-2 bg-blue-300 rounded-full text-white"
          >{{ basket.reduce((acc, item) => acc + item.qty, 0) }}</span
        >
      </div>
    </div>
    <div
      class="absolute right-5 z-10 w-56 md:w-80 p-4 origin-top-right rounded-md bg-white text-gray-800 dark:bg-slate-800 dark:text-white border dark:border-white"
      role="menu"
      aria-orientation="vertical"
      aria-labelledby="menu-button"
      tabindex="-1"
      :class="isBasketOpen ? 'block' : 'hidden'"
    >
      <div role="none" class="drop-shadow-lg">
        <ul v-show="basket.length > 0">
          <template v-for="basketItem in basket" :key="basketItem.id">
            <li
              v-show="basketItem.qty > 0"
              class="grid gap-2 grid-cols-3 pb-2 text-sm"
            >
              <span class="text-6xl z-0 pt-2">{{ basketItem.img }}</span>
              <div
                id="infopack"
                class="bg-transparent text-justify col-span-2 row-span-2 z-0"
              >
                <ul class="text-xs mx-1 space-y-1">
                  <li class="text-xl">
                    <a class="bg-blue-300 rounded-full px-4 text-white">{{
                      basketItem.name
                    }}</a>
                  </li>
                  <li
                    class="font-semibold border-b border-gray-800 dark:border-white"
                  >
                    Quantity:
                    <span class="float-right font-normal"
                      >{{ basketItem.qty }}
                    </span>
                  </li>
                  <li class="pt-1 font-semibold">
                    Calories:
                    <span class="float-right font-normal">{{
                      basketItem.nutritions.calories * basketItem.qty
                    }}</span>
                  </li>
                  <li class="font-semibold">
                    Carbohydrate:<span class="float-right font-normal"
                      >{{
                        Math.round(
                          basketItem.nutritions.carbohydrates * basketItem.qty
                        )
                      }}g</span
                    >
                  </li>
                  <li class="font-semibold">
                    Protein:<span class="float-right font-normal"
                      >{{
                        Math.round(
                          basketItem.nutritions.protein * basketItem.qty
                        )
                      }}g</span
                    >
                  </li>
                  <li class="font-semibold">
                    Fat:<span class="float-right font-normal"
                      >{{
                        Math.round(basketItem.nutritions.fat * basketItem.qty)
                      }}g</span
                    >
                  </li>
                  <li class="font-semibold">
                    Fructose:<span class="float-right font-normal"
                      >{{
                        Math.round(
                          basketItem.nutritions.sugar * basketItem.qty
                        )
                      }}g</span
                    >
                  </li>
                  <div class="space-x-2">
                    <button
                      class="bg-blue-300 hover:bg-blue-400 text-white font-bold py-2 px-4 rounded-full"
                      @click="basketItem.qty--"
                    >
                      -
                    </button>
                    <button
                      class="bg-blue-300 hover:bg-blue-400 text-white font-bold py-2 px-4 rounded-full"
                      @click="basketItem.qty++"
                    >
                      +
                    </button>
                  </div>
                </ul>
              </div>
            </li>
          </template>
          <li>
            <div class="pt-1.5 border-t-2 border-gray-800 dark:border-white">
              <ul>
                <li class="text-lg font-semibold">
                  Total fruits:
                  <span class="float-right font-normal">{{
                    basket.reduce((acc, item) => acc + item.qty, 0)
                  }}</span>
                </li>
                <li class="font-semibold">
                  Calories:
                  <span class="float-right font-normal">{{
                    basket.reduce(
                      (acc, item) => acc + item.nutritions.calories * item.qty,
                      0
                    )
                  }}</span>
                </li>
                <li class="font-semibold">
                  Carbohydrate:
                  <span class="float-right font-normal">{{
                    Math.round(
                      basket.reduce(
                        (acc, item) =>
                          acc + item.nutritions.carbohydrates * item.qty,
                        0
                      )
                    )
                  }}</span>
                </li>
                <li class="font-semibold">
                  Protein:
                  <span class="float-right font-normal">{{
                    Math.round(
                      basket.reduce(
                        (acc, item) => acc + item.nutritions.protein * item.qty,
                        0
                      )
                    )
                  }}</span>
                </li>
                <li class="font-semibold">
                  Fat:
                  <span class="float-right font-normal">{{
                    Math.round(
                      basket.reduce(
                        (acc, item) => acc + item.nutritions.fat * item.qty,
                        0
                      )
                    )
                  }}</span>
                </li>
                <li class="font-semibold">
                  Fructose:
                  <span class="float-right font-normal">{{
                    Math.round(
                      basket.reduce(
                        (acc, item) => acc + item.nutritions.sugar * item.qty,
                        0
                      )
                    )
                  }}</span>
                </li>
              </ul>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Basket",
  props: {
    selected: Object,
  },
  data() {
    return {
      fruits: [],
      fruitName: "",
      isBasketOpen: false,
    };
  },
  props: {
    basket: [Array, Object],
  },
  methods: {
    addFruitToBasket(fruit) {
      if (this.basket.filter((h) => h.name === fruit.name).length > 0) {
        this.basket[this.basket.findIndex((f) => f.name === fruit.name)].qty++;
      } else {
        const basketFruit = { ...fruit, qty: 1 };
        this.basket.push(basketFruit);
      }
    },
  },
  mounted() {},
};
</script>
