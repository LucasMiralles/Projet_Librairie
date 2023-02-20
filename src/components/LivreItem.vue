<script setup>
defineProps(["livre"]);
const emit = defineEmits(["deleteL", "addQ", "removeQ"]);
</script>

<template>
  <li>
    {{ livre.pourAfficher() }}
    <!-- cette fois en param du handler
         on n'utilise pas l'index dans le tableau
         mais directement l'id de la chose -->

    <button @click="$emit('deleteL', livre.id)">Supprimer</button>
    <button @click="$emit('addQ', livre)">Ajouter un exemplaire</button>
    <button @click="$emit('removeQ', livre)">Supprimer un exemplaire</button>
  </li>
</template>

<style>
/* Styles de base pour le bouton */
button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
}

/* Animation d'explosion lorsqu'on clique sur le bouton */
button:active {
  animation: explode 0.5s forwards;
}

/* Définition de l'animation */
@keyframes explode {
  0% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.5);
    opacity: 0.5;
  }
  100% {
    transform: scale(2);
    opacity: 0;
  }
}
</style>
