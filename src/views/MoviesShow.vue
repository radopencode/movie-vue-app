<script>
import axios from "axios";
export default {
  data: function () {
    return {
      movie: {},
    };
  },
  created: function () {
    axios.get("/movies/" + this.$route.params.id).then((response) => {
      console.log("movies show", response);
      this.photo = response.data;
    });
  },
  methods: {
    destroyMovie: function (movie) {
      axios.delete("/movies/" + movie.id).then((response) => {
        console.log("movies destroy", response);
        this.$router.push("/movies");
      });
    },
  },
};
</script>

<template>
  <div class="movies-show">
    <h2>{{ movie.name }}</h2>
    <p>Year: {{ movie.year }}</p>
    <p>Description: {{ movie.description }}</p>
    <router-link v-bind:to="`/movies/${movie.id}/edit`">Edit movie</router-link>
    <button v-on:click="destroyMovie(movie)">Destroy movie</button>
    <router-link to="/movies">Back to all movies</router-link>
  </div>
</template>
