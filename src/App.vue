<script>
import Slides from "./components/Slides.vue"
import Home from "./components/Home.vue";

const routes = {
  '/': Home,
  '/builder': Slides
}

export default {
  data() {
    return {
      currentPath: window.location.hash
    }
  },
  computed: {
    currentView() {
      return routes[this.currentPath.slice(1) || '/'] || NotFound
    }
  },
  mounted() {
    window.addEventListener('hashchange', () => {
      this.currentPath = window.location.hash
    })
  }
}
</script>

<template>
  <header class="header">
    <a href="#/">Home</a> |
    <a href="#/builder">Card Builder</a>
  </header>

  <main class="main">
    <component :is="currentView" />
  </main>
</template>

<style>
  .header {
    padding: 18px 15px;
  }
</style>
