<script setup>
import axios from 'axios';
import { ref } from 'vue';
import SiteHeader from '../components/SiteHeader.vue';
import SiteModal from '../components/SiteModal.vue';
import { useStore } from "../store/index.js"

const store = useStore()
const genre = ref()
const showModal = ref(false);
const selectedId = ref(0);

const openModal = (id) => {
  showModal.value = true;
  selectedId.value = id;
};

const closeModal = () => {
  showModal.value = false;
};

const getGenres = async () => {
  await store.getMovies(genre.value);
}

</script>

<template>
  <SiteHeader />
  <RouterLink to="/cart" custom v-slot="{ navigate }">
    <button @click="navigate" role="link">Cart</button>
  </RouterLink>
  <select v-model="genre" @change="getGenres()">
    <option value="28">Action</option>
    <option value="35">Comedy</option>
    <option value="16">Animation</option>
    <option value="53">Thriller</option>
    <option value="80">Fantasy</option>
  </select>
  <div class="purchase-container">
    <img v-for="movie in store.movies" :id="movie.id" @click="openModal(movie.id)" class="poster"
     :src="`https://image.tmdb.org/t/p/w500/${movie.poster}`" />
  </div>
  <SiteModal v-if="showModal" @toggleModal="closeModal()" :id="selectedId" />
</template>

<style>
.purchase-container {
  display: flex;
  flex-wrap: wrap;
}

.purchase-container>.poster {
  max-height: 42.5vh;
  max-width: 42.5vw;
  margin-left: 4%;
  margin-bottom: 2%;
  border: solid;
  border-width: 20%;
  border-radius: 4%;
  border-color: rgb(151, 186, 151);
}
</style>