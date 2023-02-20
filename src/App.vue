<script setup>
import HeaderLivre from "./components/HeaderLivre.vue";
import LivreForm from "./components/LivreForm.vue";
import LivreItem from "./components/LivreItem.vue";
import MethodeLivre from "./components/MethodeLivre.vue";
import RechercheLivre from "@/components/RechercheLivre.vue";
</script>

<template>
  <div class="home">

  <header>
 Voici le prototype de la page d'accueil de la librairie
    <HeaderLivre />
     <MethodeLivre />
   </header>
   <main>
   </main>
  </div>
 </template>

 <style scoped>
 @font-face {
   font-family: "God Of War";
   src: url("/public/GODOFWAR.TTF");
 }

 .home {
   display: flex;
   flex-direction: column;
   align-items: center;
   justify-content: center;
    height: 100vh;
   font-family: "God Of War", Arial, sans-serif;
   font-weight: bold;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
   background: url("/public/Fond.jpg");
    background-size: cover;
    background-position: center;
    background-attachment: fixed;
 }
 </style>
