<script setup>
import axios from "axios";
import { useStore } from "../store/index.js"

const store = useStore();
const props = defineProps(["id"]);
const emits = defineEmits(["toggleModal"]);

let data = (
  await axios.get(`https://api.themoviedb.org/3/movie/${props.id}`, {
    params: {
      api_key: "ab590dbfc1eb546b5263a30c390d2d07",
      append_to_response: "videos",
    }
  })).data;
</script>

<template>
  <Teleport to="body">
    <div class="modal-outer-container" @click.self="emits('toggleModal')">
      <div class="modal-inner-container">
        <button class="close-button" @click="emits('toggleModal')">X</button>
        <img class="modalPoster" :src="`https://image.tmdb.org/t/p/w500/${data.poster_path}`" width="315" height="470"
          alt="movie poster" />
        <div class="title">
          <h1>{{ data.title }}</h1>
        </div>
        <div class="description">
          <button @click="store.addToCart(props.id, {
            id: data.id,
            poster: data.poster_path,
            title: data.title,
            date: data.release_date,
            summary: data.overview,
          })">Purchase</button>
          <h3>{{ data.tagline }}</h3>
          <h4>{{ data.release_date }}</h4>
          <iframe v-if="data.videos.results.length" width="355" height="210" id="trailer"
            :src="`https://www.youtube.com/embed/${data.videos.results[0].key}`" frameborder="0"
            allowfullscreen></iframe>
        </div>
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.modal-outer-container {
  position: fixed;
  top: 0;
  left: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background: #00000099;
  z-index: 3;
}

.modal-outer-container .modal-inner-container {
  background-color: ivory;
  color: rgb(141, 187, 141);
  width: clamp(400px, 100%, 800px);
  height: 525px;
  position: relative;
  border: solid;
  border-color: ivory;
  border-radius: 2%;
  text-align: center;
}

.modal-outer-container .modal-inner-container .close-button {
  position: absolute;
  right: 0px;
  padding: 1rem;
  border: none;
  background: ivory;
  font-weight: bold;
  font-size: 1.25rem;
  color: rgb(141, 187, 141);
}

.close-button {
  margin-top: 0%;
  font-family: 'Fredoka One';
}

.description {
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-size: 16px;
  margin-right: 6%;
}
.description > button {
  margin-top: -1%;
  background-color: rgb(134, 184, 134);
  padding: 10px 40px;
  height: 40px;
  font-size: larger;
  font-family: 'Fredoka One';
  color: rgb(14, 58, 14);
  border: none;
  border-radius: 18px;
}
.modalPoster {
  float: left;
  padding: 3%;
}

.title {
  font-family: "Fredoka One";
  font-size: 16px;
  text-align: center;
  margin-right: 6%;
}

#trailer {

  margin-top: 1%;
}
</style>
