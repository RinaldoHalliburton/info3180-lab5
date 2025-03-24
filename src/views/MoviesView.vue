<template>
  <div class="container py-4">
    <h2 class="mb-4">🎞️ Movies</h2>
    <div class="row g-4">
      <div class="col-md-4" v-for="movie in movies" :key="movie.id">
        <div class="card h-100 shadow-sm">
          <img :src="movie.poster" class="card-img-top" alt="Movie Poster" />
          <div class="card-body">
            <h5 class="card-title">{{ movie.title }}</h5>
            <p class="card-text">{{ movie.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const movies = ref([]);

function fetchMovies() {
  fetch("/api/v1/movies")
    .then((res) => res.json())
    .then((data) => {
      movies.value = data.movies;
    })
    .catch((err) => {
      console.error("Failed to fetch movies:", err);
    });
}

onMounted(() => {
  fetchMovies();
});
</script>
