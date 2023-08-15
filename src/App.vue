<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
// import { useMessageStore } from './stores/message';
// import { storeToRefs } from 'pinia';
// const store = useMessageStore()
// const { message } = storeToRefs(store)
</script>

<template>
  <header class="max-h-screen leading-normal">
    <h3>Thaipat Sukhumpraisan</h3>
    <!-- <div id="flashMessage" v-if="message">
      <h4>{{ message }}</h4>
    </div> -->
    <nav class="p-8 font-bold text-slate-800 router-link-exact-active:text-green-600">
      <RouterLink :to="{name: 'EventList'}">Home</RouterLink> |
      <RouterLink :to="{name: 'about'}">About</RouterLink> |
      <RouterLink :to="{name: 'category'}">Category</RouterLink> |
      <RouterLink :to="{name: 'student'}">Student List</RouterLink>
    </nav>
  </header>

  <RouterView/>
</template>

<style>
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}

h4 {
  font-size: 20px;
}

@keyframes yellowfade {
  from {
    background: yellow;
  }
  to {
    background: transparent;
  }
}

#flashMessage {
  animation: yellowfade 3s ease-in-out;
}
</style>