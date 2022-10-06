<template>
  <label for="toggleB" class="flex items-center cursor-pointer">
    <!-- toggle -->
    <div class="relative">
      <!-- input -->
      <input
        @change="toggleTheme"
        type="checkbox"
        id="toggleB"
        class="sr-only"
      />
      <!-- Dark -->
      <div class="block bg-gray-200/50 drop-shadow-md w-14 h-8 rounded-full" />
      <!-- Light -->
      <div
        class="dot absolute left-1 top-1 bg-yellow-400 w-6 h-6 rounded-full transition"
      >
        <div class="absolute left-1 dot w-5 h-5 bg-white rounded-full"></div>
      </div>
    </div>
    <div
      class="switch-toggle"
      :class="{ 'switch-toggle-checked': userTheme === 'dark' }"
    ></div>
  </label>
</template>

<script>
export default {
  mounted() {
    const initUserTheme = this.getTheme() || this.getMediaPreference();
    this.setTheme(initUserTheme);
  },

  data() {
    return {
      userTheme: "light-theme",
    };
  },

  methods: {
    toggleTheme() {
      const activeTheme = localStorage.getItem("user-theme");
      if (activeTheme === "light-theme") {
        this.setTheme("dark");
      } else {
        this.setTheme("light-theme");
      }
    },

    getTheme() {
      return localStorage.getItem("user-theme");
    },

    setTheme(theme) {
      localStorage.setItem("user-theme", theme);
      this.userTheme = theme;
      document.documentElement.className = theme;
    },

    getMediaPreference() {
      const hasDarkPreference = window.matchMedia(
        "(prefers-color-scheme: dark)"
      ).matches;
      if (hasDarkPreference) {
        return "dark";
      } else {
        return "light-theme";
      }
    },
  },
};
</script>

<style scoped>
input:checked ~ .dot {
  transform: translateX(100%);
  background-color: rgb(255, 255, 255);
}
</style>
