<script setup>
import Movies from "../components/Movies.vue";
</script>

<template>
  <div>
    <router-link :to="{ name: 'home' }">
      <h3 class="font-bold text-xl text-center my-10">Movie Lists</h3>
    </router-link>
  </div>
  <div class="flex justify-center items-center">
    <div class="w-11/12">
      <Movies />
      <div class="text-center my-10 text-slate-500">
        Joevano &copy; {{ new Date().getFullYear("y") }}
      </div>
    </div>
  </div>
</template>
<style scoped>
.movie {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
</style>
