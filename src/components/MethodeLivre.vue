<script setup>
import { reactive, onMounted } from "vue";
import Livre from "../Livre.js";
import LivreForm from "@/components/LivreForm.vue";
import LivreItem from "@/components/LivreItem.vue";
import RechercheLivre from "@/components/RechercheLivre.vue";



const listeL = reactive([]);
const rechercheL = reactive([]);

// -- l'url de l'API
const url = "https://webmmi.iut-tlse3.fr/~pecatte/librairies/public/28/livres";

function ajouterQuantite(livre) {
  console.log(livre);
  // -- ajouter la quantité
  livre.incrementer();
  // -- entête http pour la req AJAX
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // -- la chose modifiée est envoyé au serveur
  //  via le body de la req AJAX
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({
      'id': livre.id,
      'titre': livre.titre,
      'qtestock': livre.qtestock,
      'prix': livre.prix
    }),
  };
  // -- la req AJAX
  fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        // actualiser la liste des livres
        getLivres();
      })
      .catch((error) => console.log(error));
}
function enleverQuantite(livre) {
  console.log(livre);
  // -- enlever la quantité
  livre.decrementer();
  // -- entête http pour la req AJAX
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // -- la chose modifiée est envoyé au serveur
  //  via le body de la req AJAX
  const fetchOptions = {
    method: "PUT",
    headers: myHeaders,
    body: JSON.stringify({
      'id': livre.id,
      'titre': livre.titre,
      'qtestock': livre.qtestock,
      'prix': livre.prix
    }),
  };
  // -- la req AJAX
  fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        if(livre.qtestock == 0){
          supprimerLivre(livre.id);
        }
        // actualiser la liste des livres
        getLivres();
      })
      .catch((error) => console.log(error));
}
// -- handle pour supprimer un livre à partir de son id
function supprimerLivre(id) {
  console.log(id);
  const fetchOptions = {
    method: "DELETE",
  };
  // -- l'id du livre à supprimer doit être
  //  ajouté à la fin de l'url
  fetch(url + "/" + id, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        getLivres();
        rechercherLivre()
      })
      .catch((error) => console.log(error));
}
// -- handle pour ajouter une nouveau livre à partir du libelle saisi dans le formulaire
function ajouterLivre(titre, qtestock, prix) {
  console.log(titre);
  console.log(qtestock);
  console.log(prix);
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // --  le libelle du nouveau livre est envoyé au serveur
  //  via le body de la req AJAX
  const data = {titre: titre, qtestock: qtestock, prix: prix};
  const fetchOptions = {
    method: "POST",
    headers: myHeaders,
    body: JSON.stringify(data),
  };
  fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        getLivres();
      })
      .catch((error) => console.log(error));
}
// -- req AJAX pour récupérer les todos
//    et les stocker dans le state listeL
function getLivres() {
  const fetchOptions = { method: "GET" };
  fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        // -- vider la liste des livres
        listeL.splice(0, listeL.length);
        // pour chaque donnée renvoyée par l'API
        //  créer un objet instance de la classe Livre
        //  et l'ajouter dans la liste listeL
        dataJSON.forEach((v) => listeL.push(new Livre(v.id, v.titre, v.qtestock, v.prix)));
      })
      .catch((error) => console.log(error));
}
function rechercherLivre(motcle) {
  const fetchOptions = { method: "GET" };
  fetch(url + "?search=" + motcle, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        // -- vider la liste des livres
        rechercheL.splice(0, rechercheL.length);
        // pour chaque donnée renvoyée par l'API
        //  créer un objet instance de la classe Livre
        //  et l'ajouter dans la liste listeL
        dataJSON.forEach((v) => rechercheL.push(new Livre(v.id, v.titre, v.qtestock, v.prix)));
      })
      .catch((error) => console.log(error));
}
// -- fonction du cycle de vie du composant
// exécutée 1 seule fois à la création
onMounted(() => {
  getLivres();
});

</script>

<template>
  <h3>Liste des livres de la librairie (Vous pouvez également y rajouter un livre en remplissant le formulaire)</h3>
  <LivreForm @addL="ajouterLivre"></LivreForm>
  <ul>
    <LivreItem
        v-for="livre of listeL"
        :key="livre.id"
        :livre="livre"
        @deleteL="supprimerLivre"
        @addQ="ajouterQuantite"
        @removeQ="enleverQuantite"
    />
  </ul>
  <h3>Rechercher un livre dans la librairie</h3>
  <RechercheLivre @searchL="rechercherLivre"></RechercheLivre>
  <ul>
    <LivreItem
        v-for="livre of rechercheL"
        :key="livre.id"
        :livre="livre"
        @deleteL="supprimerLivre"
        @addQ="ajouterQuantite"
        @removeQ="enleverQuantite"
    />
  </ul>
</template>
<style scoped>
</style>
