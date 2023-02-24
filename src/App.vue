<script setup>
import HeaderLivre from "./components/HeaderLivre.vue";
import MethodeLivre from "./components/MethodeLivre.vue";
</script>

<template>
  <div class="background">
     <HeaderLivre />
    <div class="liste">
      <MethodeLivre />
    </div>
  </div>
 </template>

 <style scoped>

 .background {
   display: flex;
   flex-direction: column;
   align-items: center;
   background: url("/public/img/Geralt.jpg!d");
   background-size: cover;
   background-position: center;
   background-attachment: fixed;
 }

 .liste{
   display: flex;
   flex-direction: column;
   align-items: center;
   font-family: "Trajan", Arial, sans-serif;
   font-size: 20px;
   color: #eee7e7;
   font-weight: bold;
   -webkit-font-smoothing: antialiased;
   -moz-osx-font-smoothing: grayscale;
 }

 </style>
