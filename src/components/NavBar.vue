<template>
  <div id="nav" class="sticky top-0">
    <nav
      class="flex flex-wrap items-center justify-between w-full py-3 md:py-0 px-3 text-lg text-gray-70 bg-white shadow-lg"
    >
      <div>
        <a href="/" class="md:p-4 py-2 block pr-4 pl-3 text-black-800 text-xl"
          >Something</a
        >
      </div>

      <svg
        xmlns="http://www.w3.org/2000/svg"
        id="menu-button"
        class="h-6 w-6 cursor-pointer md:hidden block"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M4 6h16M4 12h16M4 18h16"
        />
      </svg>

      <div class="hidden w-full md:flex md:items-center md:w-auto" id="menu">
        <ul
          class="pt-4 text-base text-gray-700 md:flex md:justify-between md:pt-0"
        >
          <li>
            <router-link
              to="/"
              class="md:p-4 py-2 block pr-4 pl-3 text-gray-800 hover:text-black-300"
              >Home</router-link
            >
          </li>
          <li>
            <router-link
              to="/about"
              class="md:p-4 py-2 block pr-4 pl-3 text-gray-800 hover:text-black-300"
              >About</router-link
            >
          </li>
        </ul>
      </div>
    </nav>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  setup() {
    return {};
  },
});
</script>

<style>
nav {
  padding: 30px;
  width: 100%;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #2c3e50;
  border-bottom: 2px solid #2c3e50;
}
</style>
