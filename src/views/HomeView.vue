<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: {},
      newMovieParams: {},
      errors: [],
    };
  },
  created: function () {
    this.showMovies();
  },
  methods: {
    showMovies: function () {
      axios.get("/movies.json").then((response) => {
        this.movies = response.data;
        console.log("All movies", this.movies);
      });
    },
    createMovie: function () {
      axios.post("/movies.json", this.newMovieParams).then((response) => {
        console.log(response.data);
      });
    },
  },
};
</script>

<template>
  <div v-for="movie in movies" v-bind:key="movie.id">
    <h1>{{ movie.title }}</h1>
    <p>{{ movie.year }}</p>
    <button>More info</button>
  </div>
  <div>
    <form v-on:submit.prevent="createMovie()">
      <h1>New Movie</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newMovieParams.title" />
      </div>
      <div>
        <label>Year:</label>
        <input type="text" v-model="newMovieParams.year" />
      </div>
      <div>
        <label>Plot:</label>
        <input type="text" v-model="newMovieParams.plot" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style></style>
