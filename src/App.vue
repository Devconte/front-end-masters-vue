<script setup>
import { ref } from "vue";

const charactersList = ref([
  { name: "Naruto", favorite: false },
  { name: "Sasuke", favorite: false },
  { name: "Sakura", favorite: false },
  { name: "Kiba", favorite: false },
  { name: "Kakashi", favorite: false }
]);

const favoriteCharacters = ref([]);

const addToFavorite = (character) => {
  character.isFavorite = true;
  favoriteCharacters.value.push(character);
};

const addCharacter = (event) => {
  event.preventDefault();
  const name = event.target.name.value;
  const newCharacter = { name, favorite: false };
  charactersList.value.push(newCharacter);
  event.target.reset();
};
</script>

<template>
  <form @submit="addCharacter">
    <label for="name">Add a character</label>
    <input type="text" id="name" name="name" v-model="newCharacterName"/>
    <button type="submit" >Submit</button>
  </form>

  <h1> Naruto </h1>
  <p v-if="charactersList.length === 0"> There are no characters</p>
  <ul v-else>
    Characters list
    <li v-for="character in charactersList" :key="character.name">
      {{ character.name }}
      <button @click="addToFavorite(character)">add to favorite</button>
    </li>
  </ul>
  <p v-if="favoriteCharacters.length === 0">No favorite character</p>
  <ul v-else>
    Favorite Characters
    <li v-for="favCharacter in favoriteCharacters" :key="favCharacter.name">
      {{ favCharacter.name }}
    </li>
  </ul>
</template>



