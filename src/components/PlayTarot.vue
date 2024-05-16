<script setup>
import { ref, reactive } from "vue";
const shuffle = ref(false);
const showCard = ref(false);
const showDescriptionCard = ref(false);
let tarotCardSelected = reactive(ref());
let tarotCardShow = reactive(ref(""));
let srcTarot = reactive(ref(""));

const shuffleDraw = () => {
  shuffle.value = true;
  showCard.value = false;
  showDescriptionCard.value = false;
  tarotCardShow.value = "";
  setTimeout(() => {
    shuffle.value = false;
  }, "3000");

  fetch("https://tarotapi.dev/api/v1/cards/random?n=1")
    .then((res) => res.json())
    .then(function (res) {
      console.log(res);

      setTimeout(() => {
        showCard.value = true;
      }, "3100");
      setTimeout(() => {
        showDescriptionCard.value = true;
      }, "4100");

      tarotCardSelected.value = res;
      tarotCardShow = tarotCardSelected.value.cards[0];
      imageCard();
    })
    .catch((err) => console.log(err));
};

function imageCard() {
  if (tarotCardShow != "") {
    if (tarotCardShow.suit) {
      srcTarot =
        "../images/cards/" +
        tarotCardShow.suit +
        "/" +
        tarotCardShow.value_int +
        ".jpg";
    } else {
      srcTarot = "../images/cards/" + tarotCardShow.value_int + ".jpg";
    }
  }

  return srcTarot;
}
</script>
<template>
  <v-container class="fill-height align-content-start">
    <v-card class="mx-auto vcard" prepend-icon="mdi-cards-playing">
      <template v-slot:title>
        <span class="font-weight-black">Play Tarot!</span>
      </template>

      <v-card-text class="bg-surface-light pt-4 text-center height">
        <div class="info mb-6">
          Take a couple of deep breaths and relax. Clear your mind. Think about
          what area of your life needs guidance or of a problem that you would
          like to solve. <br />Then, when you are ready, click on the button
          bellow "Shuffle the Deck and draw a Card".
        </div>
        <v-btn @click="shuffleDraw" color="deep-purple"
          >Shuffle the Deck and draw a Card
        </v-btn>
        <div class="deckArea mb-6">
          <div class="tarotCard">
            <div class="card-wrapper cardArea">
              <ul
                class="card-list mt-6 mb-6"
                :class="[shuffle ? 'is-animated' : '']"
              >
                <li class="card-list__item" data-card="0">
                  <div class="card"></div>
                </li>
                <li class="card-list__item" data-card="1">
                  <div class="card"></div>
                </li>
                <li class="card-list__item" data-card="2">
                  <div class="card"></div>
                </li>
                <li class="card-list__item" data-card="3" v-if="showCard">
                  <div class="card">
                    <img
                      :src="imageCard()"
                      class="animate__animated animate__flipInY"
                    />
                  </div>
                </li>
              </ul>
            </div>
          </div>
          <div class="tarotMeaning">
            <div v-if="showDescriptionCard">
              <h2 class="mb-4 coloryellow">{{ tarotCardShow.name }}</h2>

              <h3 class="mb-3">
                <span class="coloryellow">Suit:</span>
                {{ tarotCardShow.suit || " - " }} |
                <span class="coloryellow">Type:</span>
                {{ tarotCardShow.type }}
              </h3>
              <h3 class="mb-3">
                <span class="coloryellow">Description:</span>
                {{ tarotCardShow.desc }}
              </h3>

              <h3>
                <span class="coloryellow">Meaning:</span>
                {{ tarotCardShow.meaning_up }}
              </h3>
            </div>
          </div>
        </div>
      </v-card-text>
    </v-card>
  </v-container>
</template>

<style scoped>
.coloryellow {
  color: #f0d87a;
}
.info {
  font-size: 1.2rem;
}
.vcard {
  width: 100%;
}
.deckArea {
  width: 100%;
  height: 400px;
}
.tarotCard {
  width: 40%;

  float: left;
  height: 400px;
}
.cardArea {
  width: 100%;
  max-width: 200px;
  margin: 0 auto;
}
.tarotMeaning {
  width: 58%;
  float: left;
  padding: 1%;
  height: 380px;
  text-align: left;
  overflow: auto;
  margin-top: 20px;
}
@media (max-width: 768px) {
  .deckArea {
    width: 100%;
    height: auto;
  }
  .tarotCard {
    width: 100%;
    height: 300px;
  }
  .tarotMeaning {
    width: 98%;
    height: 520px;
  }
  .height {
    height: 1100px;
  }
}
@keyframes shuffle {
  0% {
    transform: rotate(0) translateX(0) scale(1);
  }
  50% {
    transform: rotate(5deg) translateX(105%) scale(0.96);
  }
  100% {
    transform: rotate(0) translateX(0);
  }
}
.card-wrapper {
  display: flex;
  flex-direction: row;
  height: 350px;
}
.card-list {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
  max-height: 100%;
  height: 350px;
  margin: 0;
  padding: 30px;
  list-style: none;
}
.card-list__item {
  position: absolute;
  animation: none;
  animation-fill-mode: forwards;
}
.card-list__item[data-card="0"] {
  z-index: 6;
  margin-top: 0;
}
.card-list__item[data-card="1"] {
  z-index: 5;
  margin-top: 4px;
}
.card-list__item[data-card="2"] {
  z-index: 4;
  margin-top: 8px;
}
.card-list__item[data-card="3"] {
  z-index: 8;
  margin-top: 0px;
}
.card-list__item[data-card="3"] img {
  width: 100%;
  height: 100%;
}
.card-list__item[data-card="3"] .card {
  padding: 0 !important;
}
.is-animated .card-list__item[data-card="0"] {
  animation: shuffle 1s ease-in-out 0s 1 normal;
  z-index: 2;
  transition: z-index 0s ease-in-out 0.5s;
}
.is-animated .card-list__item[data-card="1"] {
  animation: shuffle 1s ease-in-out 1s 1 normal;
  z-index: 1;
  transition: z-index 0s ease-in-out 1.5s;
}
.is-animated .card-list__item[data-card="2"] {
  animation: shuffle 1s ease-in-out 2s 1 normal;
  z-index: 0;
  transition: z-index 0s ease-in-out 2.5s;
}
.card {
  display: flex;
  max-width: 100%;
  width: 150px;
  max-height: 100%;
  height: 250px;
  padding: 30px;
  border-radius: 15px;
  box-shadow: 0 1px 3px 0 #222;
  background: #555;
}
[data-card="0"] .card {
  background: url("../assets/images/tarot_back1.png") center center;
  background-size: cover;
}
[data-card="1"] .card {
  background: url("../assets/images/tarot_back2.png") center center;
  background-size: cover;
}
[data-card="2"] .card {
  background: url("../assets/images/tarot_back3.png") center center;
  background-size: cover;
}
</style>
