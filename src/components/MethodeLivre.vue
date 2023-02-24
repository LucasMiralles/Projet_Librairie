<script setup>
import { reactive, onMounted } from "vue";
import Livre from "../Livre.js";
import LivreForm from "@/components/LivreForm.vue";
import LivreItem from "@/components/LivreItem.vue";
import RechercheLivre from "@/components/RechercheLivre.vue";



const listeL = reactive([]);
const rechercheL = reactive([]);

// l'url de l'API
const url = "https://webmmi.iut-tlse3.fr/~pecatte/librairies/public/28/livres";

function ajouterQuantite(livre) {
  console.log(livre);
  // ajouter la quantité
  livre.incrementer();
  // entête http pour la req AJAX
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // la quantité modifiée est envoyé au serveur
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
  // la requête AJAX
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
  // enlever la quantité
  livre.decrementer();
  // entête http pour la req AJAX
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // la quantité modifiée est envoyé au serveur
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
  // la requête AJAX
  fetch(url, fetchOptions)
      .then((response) => {
        return response.json();
      })
      .then((dataJSON) => {
        console.log(dataJSON);
        if(livre.qtestock === 0){
          supprimerLivre(livre.id);
        }
        // actualiser la liste des livres
        getLivres();
      })
      .catch((error) => console.log(error));
}

// supprimerLivre pour supprimer un livre à partir de son id
function supprimerLivre(id) {
  console.log(id);
  const fetchOptions = {
    method: "DELETE",
  };
  // -- l'id du livre à supprimer doit être ajouté à la fin de l'url
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

// ajouterLivre pour ajouter une nouveau livre à partir du formulaire de saisie
function ajouterLivre(titre, qtestock, prix) {
  console.log(titre);
  console.log(qtestock);
  console.log(prix);
  let myHeaders = new Headers();
  myHeaders.append("Content-Type", "application/json");
  // les données du nouveau livre sont envoyées au serveur
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

// requête AJAX pour récupérer les livres et les stocker dans la listeL
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
        //  et l'ajouter dans la liste rechercheL
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
  <h3>Ajoutez un elixir pour accroître les pouvoirs du Sorceleur </h3>
  <LivreForm @addL="ajouterLivre"></LivreForm>
  <ul>
    <div class="disposition">
      <LivreItem
          v-for="livre of listeL"
          :key="livre.id"
          :livre="livre"
          @deleteL="supprimerLivre"
          @addQ="ajouterQuantite"
          @removeQ="enleverQuantite"
      />
    </div>
  </ul>
  <h3>Rechercher un elixir parmis la collection du Sorceleur</h3>
  <RechercheLivre @searchL="rechercherLivre"></RechercheLivre>
  <ul>
    <div class="recheche-disposition">
    <LivreItem
        v-for="livre of rechercheL"
        :key="livre.id"
        :livre="livre"
        @deleteL="supprimerLivre"
        @addQ="ajouterQuantite"
        @removeQ="enleverQuantite"
    />
    </div>
  </ul>
</template>

<style scoped>

h3 {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(0, 0, 0, 0.7);
  padding: 10px;
  font-family: "The Witcher", Arial, sans-serif;
  font-size: 20px;
  color: #eee7e7;
  text-align: center;
  text-shadow: #988f8f 10px 5px 10px;
  margin-top: 50px;
}

.disposition{
  display: grid;
  flex-direction: row;
  flex-wrap: wrap;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  margin-top: 20px;
}

.recheche-disposition{
  display: grid;
  flex-direction: row;
  flex-wrap: wrap;
  grid-template-columns: 1fr 1fr 1fr 1fr;
  margin-top: 20px;
}

</style>
