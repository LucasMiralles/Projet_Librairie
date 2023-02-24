<script setup>
defineProps(["livre"]);
const emit = defineEmits(["deleteL", "addQ", "removeQ"]);
</script>

<template>
  <li>
    <div class="livre">
      <div class="livre-item">
        <h1 class="titre">{{ livre.titre }}</h1>
        <div class="stock">
          <p> Stock : <span class="quantite">{{livre.qtestock}}</span></p>
          <div class="bouttons">
          <button class="boutton" @click="$emit('addQ', livre)">+</button>
          <button class="boutton" @click="$emit('removeQ', livre)">-</button>
          </div>
          <div class="supprimer">
            <button class="boutton-sup" @click="$emit('deleteL', livre.id)"><img src="/public/img/mort.ico" alt="icône tête de mort"></button>
          </div>
        </div>
        <div class="prix">
          <p class="prix-euros">{{ livre.prix }}<img class="orin" src="/public/img/orin.ico" alt="icône monnaie The Witcher"></p>
        </div>
      </div>
    </div>
  </li>
</template>

<style>

button {
  background-color: #2d2d2d;
  border: 0 solid #333333;
  border-radius: 10px;
  color: #ffffff;
  font-size: 14px;
  font-family: 'The Witcher', serif;
  box-shadow: 2px 2px 0 #000000;
  cursor: pointer;
  margin: 10px;
  padding: 8px 16px;
  transition: all 0.3s ease;
}

button:hover {
  background-color: #1c1c1c;
  box-shadow: 10px 10px 10px #000000;
}
ul {
  list-style-type: none;
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.livre{
  background-image: url("/public/img/potion.png");
  background-position: center;
  background-size: cover;
  border-radius: 20px;
  margin-right: 40px;
  width: 200px;
  height: 250px;
  padding: 20px;
  margin-bottom: 20px;
}

.livre-item{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.titre{
  font-size: 20px;
  font-weight: bold;
  font-family: "The Witcher", sans-serif;
  text-shadow: rgba(74, 131, 68, 0.85) 5px 0 5px;
  color: rgba(19, 126, 6, 0.85);
  display: flex;
  margin-top: -10px;
  justify-content: center;
  text-align: center;
}

.stock{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-size: 20px;
  font-weight: bold;
  font-family: "The Witcher", sans-serif;
  text-shadow: rgba(74, 131, 68, 0.85) 5px 0 5px;
  color: rgb(238, 231, 231);
  margin-left: -10px;
  margin-top: 20px;
}

.bouttons{
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

img{
  width: 40px;
  height: 40px;
}

.prix{
  display: flex;
  margin-top: -40px;
  margin-left: -5px;
}

.orin{
  width: 20px;
  height: 20px;
  margin-left: 5px;
  margin-bottom: -3px;
}

</style>
