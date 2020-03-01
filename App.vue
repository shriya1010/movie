<template>
  <div class="App">
    <Header :title="'Looking for your favorite movie? Enter Here!'"/>
    <Search :search="state.search" @search="handleSearch"/>
    <div class="movies">
      <Movie v-for="movie in state.movies" :movie="movie" :key="movie.imdbID"/>
    </div>
  </div>
</template>

<script>
import { reactive, watch } from "@vue/composition-api";
import Header from "./components/Header.vue";
import Search from "./components/Search.vue";
import Movie from "./components/Movie.vue";

const API_KEY = "4d4ac397";

export default {
  name: "app",
  components: {
    Header,
    Search,
    Movie
  },
  setup() {
    const state = reactive({
      search: "Harry Potter",
      loading: true,
      movies: [],
      temp: [],
      errorMessage: null
    });

    watch(() => {
      const MOVIE_API_URL = `https://www.omdbapi.com/?s=${
        state.search
      }&apikey=${API_KEY}`;
      const MOVIE_API_URL1 = `https://www.omdbapi.com/?t=${
        state.search
      }&apikey=${API_KEY}`;

      fetch(MOVIE_API_URL)
        .then(response => response.json())
        .then(jsonResponse => {
          state.movies = jsonResponse.Search;
          //state.loading = false;
        });
      fetch(MOVIE_API_URL1)
        .then(response => response.json())
        .then(jsonResponse => {
          state.temp = jsonResponse.Search;
          state.loading = false;
        });
    });

    return {
      state,
      handleSearch(searchTerm) {
        state.loading = true;
        state.search = searchTerm;
      }
    };
  }
};
</script>
