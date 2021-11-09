<template>
  <div class="modal-container">
    <img :src="foundMovie.posterUrlPreview" alt="" class="modal-poster" />
    <div class="modal-movie">
      <div class="modal-movie-table">
        <span>Оригинальное название </span>
        <span>{{ foundMovie.nameOriginal ? foundMovie.nameOriginal : foundMovie.nameRu }}</span>
        <span>Год </span>
        <span> {{ foundMovie.year }} </span>
        <span>Страна </span>
        <span>{{ countries }}</span>
        <span>Время </span>
        <span>{{ foundMovie.filmLength }} мин</span>
        <span>Жанр </span>
        <span>{{ genres }}</span>
      </div>
      <div class="rating-container">
        <span class="rating-kinopoisk">
          <a href="https://www.imdb.com/?ref_=nv_home" target="_blank">
            <img class="rating-imdb-pic" src="img/imdb.jpg" alt="" />
          </a>
          <span class="rating-number" title="Рейтинг IMDB"> {{ foundMovie.ratingImdb }} </span>
          <span class="rating-count" title="Количество голосов"> {{ foundMovie.ratingImdbVoteCount }}</span>
        </span>
        <span class="rating-mdb">
          <a :href="foundMovie.webUrl" target="_blank">
            <img class="rating-kinopoisk-pic" src="img/kinopoisk2.png" alt="" />
          </a>
          <span class="rating-number" title="Рейтинг Кинопоиск">{{ foundMovie.ratingKinopoisk }} </span>
          <span class="rating-count" title="Количество голосов"> {{ foundMovie.ratingKinopoiskVoteCount }} </span>
        </span>

        <span class="rating-age" title="Ограничение по возрасту">{{
          foundMovie.ratingAgeLimits ? foundMovie.ratingAgeLimits.slice(3) + "+" : "-"
        }}</span>
      </div>
      <p class="modal-movie-description">{{ foundMovie.description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "MovieInfo",
  data() {
    return {};
  },
  props: {
    foundMovie: Object,
  },
  computed: {
    genres() {
      return this.foundMovie.genres.map((itemGenre) => itemGenre.genre).join(" • ");
    },
    countries() {
      return this.foundMovie.countries.map((itemCountry) => itemCountry.country).join(" • ");
    },
  },
  methods: {},
};
</script>

<style lang="scss"></style>
