<template>
  <form class="search">
    <input type="text" size="30" :placeholder="movieTitle" @keyup="handleChange">
    <input @click="handleSubmit" type="submit" class="btn btn-outline-dark" value="SEARCH">
    <br>
    <br>
  </form>
</template>

<script>
import { ref } from "@vue/composition-api";

export default {
  name: "Search",
  props: ["search"],
  setup({ search }, { emit }) {
    const movieTitle = ref(search);

    return {
      movieTitle,
      handleSubmit(event) {
        event.preventDefault();
        emit("search", movieTitle.value);
      },
      handleChange(event) {
        movieTitle.value = event.target.value;
      }
    };
  }
};
</script>
