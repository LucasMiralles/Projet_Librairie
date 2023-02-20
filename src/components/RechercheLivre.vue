<script setup>
defineProps(["livre"]);
const emit = defineEmits(["searchL"]);
</script>

<template>
    <form @submit.prevent="$emit('searchL', motcle)">
      <input type="text" v-model="motcle" placeholder="Quel livre ?" />
      <input type="submit" value="Rechercher" />
    </form>
</template>

<style scoped>

</style>