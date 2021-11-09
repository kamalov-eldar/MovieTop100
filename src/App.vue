<template>
  <div id="app">
    <div class="movie-container">
      <h1>100 популярных фильмов</h1>

      <ul class="movie-list">
        <li v-for="movie in top100Films" :key="movie.filmId">
          <MovieItem v-bind:movie="movie"> </MovieItem>
        </li>
      </ul>
      <div class="overflow-auto">
        <div class="mt-3">
          <b-pagination v-model="curenModelPage" pills :total-rows="rows" size="lg" align="center"></b-pagination>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import MovieItem from "./components/MovieItem.vue";

const API_KEY = "8ccb0f71-adf6-4b8f-9927-980b4f08e9d5";

export default {
  name: "App",
  components: {
    MovieItem,
  },
  data: () => {
    return {
      top100Films: [],
      info: null,
      rows: 100,
      currentPage: 1,
    };
  },
  methods: {
    async getFilms(numberPage) {
      const responce = await fetch(`https://kinopoiskapiunofficial.tech/api/v2.2/films/top?type=TOP_100_POPULAR_FILMS&page=${numberPage}`, {
        headers: {
          "Content-Type": "aplication/json",
          "X-API-KEY": API_KEY,
        },
      });
      const data = await responce.json();
      this.top100Films = data.films;
    },
  },
  mounted: function () {
    this.getFilms(1);
  },
  computed: {
    curenModelPage: {
      get() {
        return this.currentPage;
      },
      set(numberPage) {
        this.getFilms(numberPage);
      },
    },
  },
};
</script>

<style scoped></style>
