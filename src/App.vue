<script setup>
import { ref,computed } from "vue";

const charactersList = ref([
  { name: "Naruto", favorite: false, element: "Wind" },
  { name: "Sasuke", favorite: false, element: "Fire" },
  { name: "Sakura", favorite: false, element: "Earth" },
  { name: "Kiba", favorite: false, element: "Earth" },
  { name: "Kakashi", favorite: false, element: "Lightning" }
]);

const favoriteCharacters = ref([]);

const addToFavorite = (character) => {
  character.isFavorite = true;
  favoriteCharacters.value.push(character);
};

const addCharacter = (event) => {
  event.preventDefault();
  const name = event.target.name.value;
  const newCharacter = { name, favorite: false, element: "Wind" };
  charactersList.value.push(newCharacter);
  event.target.reset();
};

const elementCounts = computed(() => {
  const counts = {
    Wind: 0,
    Fire: 0,
    Earth: 0,
    Lightning: 0,
  };

  charactersList.value.forEach(character => {
    counts[character.element]++;
  });

  return counts;
});

// Now you can access the counts for each element like this:
const WindUser = computed(() => elementCounts.value.Wind);
const FireUser = computed(() => elementCounts.value.Fire);
const EarthUser = computed(() => elementCounts.value.Earth);
const LightningUser = computed(() => elementCounts.value.Lightning);

</script>

<template>
  <form @submit="addCharacter">
    <label for="name">Add a character</label>
    <input type="text" id="name" name="name" v-model="newCharacterName"/>
    <button type="submit" >Submit</button>
  </form>

  <h1> Wind User: {{ WindUser }}</h1>
  <h1> Fire User: {{ FireUser }}</h1>
  <h1> Earth User: {{ EarthUser }}</h1>
  <h1> Lightning User: {{ LightningUser }}</h1>

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



