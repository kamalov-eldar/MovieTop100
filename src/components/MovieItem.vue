<template>
  <b-card>
    <div class="poster">
      <img :src="movie.posterUrlPreview" alt="" class="poster-img" @click="modalPoster = !modalPoster" />
    </div>
    <b-modal v-if="foundMovie !== undefined" v-model="isShowModal" size="xl" hide-footer>
      <template #modal-title>
        <h5 class="modal-title">{{ foundMovie.nameRu }}</h5>
      </template>
      <MovieInfo :found-movie="foundMovie"></MovieInfo>
    </b-modal>

    <b-modal v-model="modalPoster" hide-footer hide-header>
      <img :src="movie.posterUrlPreview" alt="" class="poster-big" />
    </b-modal>

    <div class="movie">
      <div class="movie-head">
        <h2 class="movie-title">{{ movie.nameRu }}</h2>
        <span class="b-rating-icon" title="Рейтинг Кинопоиск"
          ><svg
            viewBox="0 0 16 16"
            width="1em"
            height="1em"
            focusable="false"
            role="img"
            aria-label="star fill"
            xmlns="http://www.w3.org/2000/svg"
            fill="currentColor"
            class="bi-star-fill b-icon bi"
          >
            <g>
              <path
                d="M3.612 15.443c-.386.198-.824-.149-.746-.592l.83-4.73L.173 6.765c-.329-.314-.158-.888.283-.95l4.898-.696L7.538.792c.197-.39.73-.39.927 0l2.184 4.327 4.898.696c.441.062.612.636.283.95l-3.523 3.356.83 4.73c.078.443-.36.79-.746.592L8 13.187l-4.389 2.256z"
              ></path>
            </g></svg
          >{{ movie.rating }}</span
        >
      </div>
      <div class="movie-desciption">
        <div class="movie-table">
          <span>{{ movie.nameEn }} • {{ movie.year }}</span>
          <span>{{ countries }}</span>
          <span>{{ genres }}</span>
          <span> </span>
        </div>
        <b-button class="movie-about" size="md" block variant="outline-primary" @click="getFilm()">Подробнее</b-button>
      </div>
    </div>
  </b-card>
</template>

<script>
import MovieInfo from "./MovieInfo.vue";

const API_KEY = "8ccb0f71-adf6-4b8f-9927-980b4f08e9d5";

export default {
  name: "MovieItem",
  components: { MovieInfo },
  data() {
    return {
      modalPoster: false,
      foundMovie: undefined,
      isShowModal: true,
    };
  },
  props: {
    movie: Object,
  },
  computed: {
    genres() {
      return this.movie.genres.map((itemGenre) => itemGenre.genre).join(" / ");
    },
    countries() {
      return this.movie.countries.map((itemCountry) => itemCountry.country).join(" / ");
    },
    posterBg() {
      return {
        "background-image": `url(${this.movie.posterUrlPreview})`,
      };
    },
  },
  methods: {
    async getFilm() {
      if (this.foundMovie === undefined) {
        let movieId = this.movie.filmId;
        const responce = await fetch(`https://kinopoiskapiunofficial.tech/api/v2.2/films/${movieId}`, {
          headers: {
            "Content-Type": "aplication/json",
            "X-API-KEY": API_KEY,
          },
        });
        const data = await responce.json();
        this.foundMovie = data;
      }
      this.isShowModal = true;
    },
  },
};
</script>

<style lang="scss"></style>
