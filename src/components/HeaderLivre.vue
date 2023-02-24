<template>
    <div class="titre">
      The Library of The Witcher Universe
    </div>
      <div class="image">
        <img src="/public/img/logoW.png" alt="logo The Witcher">
      </div>
        <div class="accroche">
          Plongez dans un monde de magie, de monstres et de mystère avec The Witcher, une série de livres captivante qui vous transportera dans un univers fantastique unique
        </div>
</template>

<style scoped>

@font-face {
  font-family: "Trajan";
  src: url("/public/font/TrajanPro-Bold.otf");
}
@font-face {
  font-family: "The Witcher";
  src: url("/public/font/TheWitcher.ttf");
}

.titre {
  display: flex;
  flex-direction: column;
  align-items: center;
  background: rgba(0, 0, 0, 0.7);
  padding: 20px;
  font-family: "The Witcher", Arial, sans-serif;
  font-size: 40px;
  color: #eee7e7;
  text-align: center;
  text-shadow: #988f8f 10px 5px 10px;
}

img{
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 300px;
  height: 180px;
  padding: 30px;
  filter: grayscale(100%);
}

.accroche {
  background-color: #1C1C1C;
  color: #F5F5F5;
  padding: 20px;
  text-align: center;
  font-family: Trajan, Arial, sans-serif;
  font-size: 24px;
  font-weight: bold;
  letter-spacing: 2px;
  text-shadow: 1px 1px #000;
  max-width: 2000px;
  margin: 0 auto;
}

</style>