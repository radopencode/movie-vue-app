<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "Movies App",
      movies: [],
      newMovieParams: {},
      currentMovie: {},
    };
  },
  created: function () {
    axios.get("/movies.json").then((response) => {
      this.movies = response.data;
      console.log("All Movies", this.movies);
    });
  },
  methods: {
    createMovie: function () {
      console.log("Adding new movie.");
      axios
        .post("/movies.json", this.newMovieParams)
        .then((response) => {
          console.log("Success", response.data);
        })
        .catch((error) => console.log(error.response));
    },
    showMovie: function (movie) {
      console.log(movie);
      this.currentMovie = movie;
      document.querySelector("#movie-details").showModal();
    },
    updateMovie: function (movie) {
      var editMovieParams = movie;
      axios.patch("http://localhost:3000/movies/" + movie.id + ".json", editMovieParams).then((response) => {
        console.log("Success!", response.data);
      });
    },
    destroyMovie: function (movie) {
      axios.delete("http://localhost:3000/movies/" + movie.id).then((response) => {
        console.log("Deleted", response.data);
        var index = this.movies.indexOf(movie);
        this.movies.splice(index, 1);
      });
    },
  },
};
</script>

<template>
  <div class="home">
    <h1>{{ message }}</h1>

    <!-- Create new movie -->
    <div>
      <button v-on:click="createMovie()">Add New Movie</button>
      <div>
        <p>
          Title:
          <input type="text" v-model="newMovieParams.title" />
        </p>
      </div>
      <div>
        <p>
          Year:
          <input type="text" v-model="newMovieParams.year" />
        </p>
      </div>
      <div>
        <p>
          Description:
          <input type="text" v-model="newMovieParams.plot" />
        </p>
    </div>

    <!-- Index of Movies -->
    <div v-for="movie in movies" v-bind:key="movie.id">
      <p>Title: {{ movie.title }}</p>
      <p>Year: {{ movie.year }}</p>
      <p>Description: {{ movie.description }}</p>
      
      <!-- Show of Movie with update and destroy buttons -->
      <button v-on:click="showMovie(movie)">More Info</button>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Details</h1>
        <p>
          Title:
          <input type="text" v-model="currentMovie.title" />
        </p>
        <p>
          Year:
          <input type="text" v-model="currentMovie.year" />
        </p>
        <p>
          Description:
          <input type="text" v-model="currentMovie.description" />
        </p>
        <button v-on:click="updateMovie(currentMovie)">Update</button>
        <button v-on:click="destroyMovie(currentMovie)">Destroy</button>
        <button>Close</button>
      </form>
    </dialog>
    </div>
</template>

<style></style>
