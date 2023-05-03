<script setup>
import { ref } from "vue";
import axios from "axios";
let id = 1;
const movie = ref();

async function getMovies() {
  let data = (
    await axios.get(
      `https://api.themoviedb.org/3/movie/${id}?api_key=${
        import.meta.env.VITE_API_KEY
      }&language=en-US&append_to_response=videos`
    )
  ).data;

  movie.value = data;
  movie.value.trailer = data.videos.results.filter((trailer) => {
    return trailer.type === "Trailer";
  });
  console.log(movie.value);
}

getMovies();
</script>

<template>
  <select id="movies" @change="getMovies" v-model="id">
    <option hidden selected value="1" onclick="getSelecetedOption">Select a Movie</option>
    <option value="271110">Captain America: Civil War</option>
    <option value="317442">The Last: Naruto the Movie</option>
    <option value="812225">Black Clover: Sword of the Wizard King</option>
    <option value="98566">Teenage Mutant Ninja Turtles</option>
    <option value="635302">Demon Slayer the Movie: Mugen Train</option>
    <option value="580489">Venom: Let There Be Carnage</option>
    <option value="768744">My Hero Academia: World Heroes Mission</option>
    <option value="566525">Shang-Chi and the Legend of the Ten Rings</option>
    <option value="225745">
      Steins;Gate: The Movie - Load Region of Déjà Vu
    </option>
    <option value="475557">Joker</option>
  </select>
  <div id="container" v-if="movie">
    <h1 id="title">{{ movie.title }}</h1>
    <h2 id="Overview">{{ movie.overview }}</h2>
    <img
      id="poster"
      :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`"
    />
    <iframe
      v-if="movie.trailer"
      id="trailer"
      :src="`https://www.youtube.com/embed/${movie.trailer.at(0).key}`"
    ></iframe>
    <div class="information">
      <h3 id="Popularity">Popularity: {{ movie.popularity }}</h3>
      <h3 id="Release Date">Release Date: {{ movie.release_date }}</h3>
      <h3 id="Revenue">Revenue: {{ movie.revenue }}</h3>
      <h3 id="Runtime">Runtime: {{ movie.runtime }}</h3>
      <h3 id="Vote Average">Vote Average: {{ movie.vote_average }}</h3>
      <h3 id="Language">Language: {{ movie.original_language }}</h3>
      <h3 id="Vote Count">Vote Count: {{ movie.vote_count }}</h3>
      <h3 id="Adult">Adult: {{ movie.adult }}</h3>
      <h3 id="Budget">Budget: {{ movie.budget }}</h3>
    </div>
  </div>
</template>

<style>
@import url("https://fonts.googleapis.com/css2?family=Sedgwick+Ave+Display&display=swap");
@import url("https://fonts.googleapis.com/css2?family=Creepster&family=Dancing+Script:wght@400;700&family=Exo:wght@300&family=Londrina+Outline&family=Londrina+Solid:wght@300&family=Noto+Sans+Lepcha&family=Oswald&family=Pacifico&family=Playfair+Display&family=Playfair+Display+SC&family=Signika+Negative:wght@300&display=swap");

* {
  margin: 0;
  padding: 0;
}

body {
  background-color: black;
}

#container {
  height: 1600px;
}

#movies {
  margin-top: 30px;
}

select {
  color: white;
  text-align: center;
  margin-left: 440px;
  border: 3px solid white;
  background-color: rgb(217 49 49);
  padding: 10px;
}

#poster {
  border-radius: 50px;
  margin-left: 15%;
  height: 700px;
  margin-bottom: 50px;
  margin-top: 25px;
  border: 0px;
  border-color: white;
}

button {
  color: white;
  text-align: center;
  border: 3px solid rgb(255, 255, 255);
  background-color: rgb(217 49 49);
  padding: 10px;
}

#trailer {
  width: 70%;
  aspect-ratio: 16/9;
  margin-left: 15%;
}

h1 {
  color: white;
  margin-top: 50px;
  text-align: center;
  font-family: Abril Fatface;
  font-size: 40px;
}

h2 {
  color: white;
  text-align: center;
  margin-left: 200px;
  margin-right: 200px;
  margin-top: 25px;
  font-family: Exo;
}

h3 {
  color: white;
  font-size: 30px;
  margin-left: 730px;
  margin-bottom: 25px;
}

.information {
  transform: translateY(-1250px);
  margin-left: 40px;
}
</style>
