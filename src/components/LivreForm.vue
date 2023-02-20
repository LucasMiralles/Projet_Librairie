<script setup>
import { ref } from "vue";
// -- donnée réactive pour la saisie du libellé
const titre = ref("");
const qtestock = ref("");
const prix = ref("");

const emit = defineEmits(["addL"]);
</script>

<template>
  <form @submit.prevent="$emit('addL', titre, qtestock, prix)">
    <input type="text" v-model="titre" placeholder="Quel titre ?" />
    <input type="text" v-model="qtestock" placeholder="Quelle quantité ?" />
    <input type="text" v-model="prix" placeholder="Quel prix ?" />
    <input type="submit" value="Ajouter" />
  </form>
</template>


<style scoped>
</style>
