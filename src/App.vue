<template>
  <div>compteur: {{ count }}</div>
  <div v-if="count >= 5">Vous avez cliquer plus de 5 fois</div>
  <div v-else>Vous avez cliqué moins de 5 fois</div>
  <button @click="increment" type="submit">Incrémenter</button>
  <button @click="decriment" type="submit">decrémenter</button>
  <hr />
  <div v-html="firstName"></div>
  <hr />
  <ul>
    <li v-for="(movie, index) in movies" :key="index">
      {{ movie }}
      <button @click="deleteMovie(index)" type="submit">supprimer</button>
    </li>
  </ul>
  <button @click="sortMovie" type="submit">réorganiser</button>
  <hr />
  <form action="">
    <input
      type="text"
      name="movie"
      placeholder="enter un film"
      v-model="movieName"
    />
    <button type="submit" @click="addNewMovie">Ajouter un film</button>
  </form>
  <hr />
  <ul>
    <li>{{ person.firstName }}</li>
    <li>{{ person.lastName }}</li>
    <li>{{ person.age }}</li>
  </ul>
  <!-- prevent c'est comme si tu mettais e.preventDefault(); -->
  <button type="submit" @click.prevent="ramdonAge">changer age</button>
</template>

<script setup>
import { ref } from "vue"; // ref pour mettre à jour les variable qui va evolué au fur du temps

const count = ref(0);
const firstName = "<span>html ajouté</span>";
const movies = ref(["Titanic", "Spiderman", "Advengers"]);
const movieName = ref("");

const person = ref({
  firstName: "Djessy Flavien",
  lastName: "Tsenda",
  age: 29,
});

const decriment = () => {
  count.value--;
};
const increment = (event) => {
  console.log(event);
  count.value++;
};

const deleteMovie = (index) => {
  movies.value.splice(index, 1);
};

const sortMovie = () => {
  movies.value.sort((a, b) => a.localeCompare(b));
};

const addNewMovie = (e) => {
  e.preventDefault();
  if (movieName.value != "") {
    movies.value.push(movieName.value);
  }
  movieName.value = "";
};

const ramdonAge = () => {
  person.value.age = Math.round(Math.random() * 100);
};
</script>
