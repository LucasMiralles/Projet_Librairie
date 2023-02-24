<script setup>
defineProps(["livre"]);
const emit = defineEmits(["searchL"]);
</script>

<template>
    <form @submit.prevent="$emit('searchL', motcle)">
      <input type="text" v-model="motcle" placeholder="Élixir consommable" />
      <input type="submit" value="Rechercher" />
    </form>
</template>

<style scoped>

form {
  display: flex;
  flex-direction: row;
  align-items: center;
  background-color: #3a3a3a;
  padding: 20px;
  width: 500px;
  height: 50px;
  font-size: 18px;
  font-weight: bold;
  letter-spacing: 1px;
  border-radius: 10px;
}

input[type="text"] {
  background-color: #1C1C1C;
  color: #fff;
  border: none;
  padding: 10px;
  margin: 10px 0;
  width: 100%;
  font-size: 16px;
  border-radius: 4px;
  font-family: Trajan, serif;
}

input[type="submit"] {
  background-color: #2d2d2d;
  border: 1px solid #333333;
  border-radius: 20px;
  color: #ffffff;
  font-size: 16px;
  font-family: 'Trajan', serif;
  box-shadow: 10px 10px 10px #000000;
  cursor: pointer;
  margin: 10px;
  padding: 8px 15px;
  font-weight: bold;
  letter-spacing: 0.05em;
  transition: opacity 300ms;
}

input[type="submit"]:hover {
  -webkit-animation: glitch 750ms infinite;
}

@-webkit-keyframes glitch {
  0% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
  }
  5% {
    -moz-transform: skewX(2deg);
    -ms-transform: skewX(2deg);
    -webkit-transform: skewX(2deg);
    transform: skewX(2deg);
    opacity: 0.75;
  }
  10% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
    opacity: 1;
  }
  15% {
    -moz-transform: skewX(-5deg);
    -ms-transform: skewX(-5deg);
    -webkit-transform: skewX(-5deg);
    transform: skewX(-5deg);
    opacity: 0.75;
  }
  20% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
    opacity: 1;
  }
  45% {
    -moz-transform: skewX(3deg);
    -ms-transform: skewX(3deg);
    -webkit-transform: skewX(3deg);
    transform: skewX(3deg);
    opacity: 0.75;
  }
  50% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
    opacity: 1;
  }
  55% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
    opacity: 0.75;
  }
  60% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
    opacity: 1;
  }
  75% {
    -moz-transform: skewX(2deg);
    -ms-transform: skewX(2deg);
    -webkit-transform: skewX(2deg);
    transform: skewX(2deg);
  }
  80% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
  }
  85% {
    -moz-transform: skewX(-8deg);
    -ms-transform: skewX(-8deg);
    -webkit-transform: skewX(-8deg);
    transform: skewX(-8deg);
    opacity: 0.75;
  }
  90% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
    opacity: 1;
  }
  100% {
    -moz-transform: skewX(0deg);
    -ms-transform: skewX(0deg);
    -webkit-transform: skewX(0deg);
    transform: skewX(0deg);
  }
}

@-webkit-keyframes scan {
  0% {
    top: 0;
  }
  50% {
    top: 97%;
  }
  100% {
    top: 0;
  }
}

</style>