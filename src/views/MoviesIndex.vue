<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "";
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("/movies").then((response) => {
        console.log("movies index", response);
        this.movies = response.data;
      });
    },
  },
};
</script>

<template>
  <div class="movies-index">
    <h1>All Movies</h1>
    <div v-for="movie in movies" v-bind:key="movie.id">
      <h2>{{ movie.name }}</h2>
      <p>year: {{ movie.year }}</p>
      <p>description: {{ movie.description }}</p>
    </div>
  </div>
  <div Search by title: <input v-model="titleFilter">
<div v-for="movie in filterBy(movies, titleFilter, 'title')">
</div>
</div>
<div><!-- views/MoviesIndex.vue -->
Search by name: <input v-model="titleFilter" list="titles">
<datalist id="titles">
	<option v-for="movie in movies" v-bind:key="movie.id">{{ movie.title }}</option>
</datalist></div>
<!-- views/MoviesIndex.vue -->
<div>
	<button>Sort Alphabetically</button>
</div>
<!-- views/MoviesIndex.vue -->
<div v-for="movie in orderBy(filterBy(movies, titleFilter, 'title'), 'title')">

</template>
