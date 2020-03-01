<template>
  <div class="columns medium-6 columns large-3 columns small-12">
    <div class="movie">
      <div class="card bg-dark">
        <div class="card-divider">{{ movie.Title }}</div>
        <div class="card-section">
          <img width="100%" :alt="altText" :src="movie.Poster">
        </div>
        <div class="card-divider">
          <p>Type:{{ movie.Type }}</p>

          <p>Year:{{ movie.Year }}</p>
          <p>Link to get Poster:
            <br>
            {{ movie.Poster }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { computed } from "@vue/composition-api";

export default {
  name: "Movie",
  props: ["movie"],
  setup({ movie }) {
    const altText = computed(() => `The movie titled: ${movie.Title}`);

    return { altText };
  }

  /*setup({ temp }) {
    const altText1 = computed(() => `The movie titled: ${temp.Title}`);

    return { altText1 };
  }*/
};
</script>