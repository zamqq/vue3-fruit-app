<script>
import FruitList from "./components/FruitList.vue";
export default {
  components: {
    FruitList,
  },
};
</script>

<template>
  <div class="my-5">
    <FruitList />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin: 0;
  padding: 0;
}
</style>
