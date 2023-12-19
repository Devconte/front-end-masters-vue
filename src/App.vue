<script setup>
const charactersList = [
  { name: "Naruto" },
  { name: "Sasuke" },
  { name: "Sakura" },
  { name: "Kiba" },
  { name: "Kakashi" }
];
</script>

<template>
  <h1> Naruto </h1>
  <p v-if="charactersList.length === 0"> There are no characters</p>
  <ul v-else>Characters list
    <li v-for="character in charactersList" :key="character.name">{{ character.name }}</li>
  </ul>
</template>
