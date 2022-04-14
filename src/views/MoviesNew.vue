<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newMovieParams: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createMovie: function () {
      axios
        .post("/movies", this.newMovieParams)
        .then((response) => {
          console.log("movies create", response);
          this.$router.push("/movies");
        })
        .catch((error) => {
          console.log("movies create error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="movies-new">
    <h1>New Movie</h1>
    <form v-on:submit.prevent="createMovie()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Name:
      <input type="text" v-model="newPhotoParams.name" />
      Year
      <input type="text" v-model="newPhotoParams.year" />
      description:
      <input type="text" v-model="newPhotoParams.description" />
      <input type="submit" value="Create" />
    </form>
  </div>
</template>
