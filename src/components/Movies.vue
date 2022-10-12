<template>
  <div>
    <form @submit.prevent="test" action="">
      <div class="flex gap-0 items-center">
        <input
          class="border rounded-l-lg py-2 px-2 focus:border-blue-600 focus:outline-none transition-colors"
          type="text"
          placeholder="Search movie..."
          v-model="search"
          @keyup="searchMovie(search)"
        />
        <button
          class="border border-blue-600 py-2 px-5 rounded-r-lg bg-blue-600 text-white hover:bg-blue-500 transition-colors"
        >
          <i class="fa-solid fa-magnifying-glass"></i>
        </button>
      </div>
    </form>
    <div v-if="movies">
      <div class="movie gap-x-8 gap-y-10 mt-10">
        <div v-for="movie in movies" :key="movie.id">
          <a :href="`/movie/${movie.id}`">
            <img
              class="w-[100%] mb-5 object-cover rounded-xl hover:scale-105 transition-all"
              :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
              :alt="movie.title"
            />
          </a>
          <p>{{ movie.title }}</p>
          <p>{{ movie.release_date }}</p>
        </div>
      </div>
    </div>
    <div v-if="movies.length === 0">
      <p
        class="text-xl h-[600px] flex justify-center items-center text-slate-500"
      >
        No result found :(
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      search: "",
      movies: [],
    };
  },

  methods: {
    searchMovie(search) {
      if (search) {
        axios
          .get(
            `https://api.themoviedb.org/3/search/movie?api_key=bd4d05e79f3e765cbc73b27ff1a3d126&language=en-US&query=${search}&page=1&include_adult=false`
          )
          .then((res) => {
            this.movies = res.data.results;
          })
          .catch((err) => {
            console.error(err);
          });
      } else {
        this.defaultMovie();
      }
    },

    defaultMovie() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/popular?api_key=bd4d05e79f3e765cbc73b27ff1a3d126"
        )
        .then((res) => {
          this.movies = res.data.results;
        })
        .catch((err) => {
          console.error(err);
        });
    },
  },

  created() {
    this.defaultMovie();
  },
};
</script>
<style scoped>
.movie {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
</style>
