<template>
  <div class="bg-gray-200 items-stretch h-screen overflow-hidden">
    <Navbar />
    <router-view class="mb-auto h-[89%]" />
    <Footer />
  </div>
</template>
<script lang="ts">
import { defineComponent } from "vue";
import Navbar from "./components/NavBar.vue";
import Footer from "./components/Footer.vue";

export default defineComponent({
  components: {
    // HomeView,
    Navbar,
    Footer,
  },
  setup() {
    return {};
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #e5e7eb;
}
</style>
