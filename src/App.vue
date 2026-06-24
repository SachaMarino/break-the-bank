<script>
import Home from "./pages/Home.vue";
import Game from "./pages/Game.vue";
import Lose from "./pages/Lose.vue";
import Win from "./pages/Win.vue";
import BorderMainSvg from "./components/svg/borderDesign/BorderMain.svg.vue";
import NumberOrder from "./components/mini-games/NumberOrder.vue";
export default {
  components: {
    Home,
    Game,
    Lose,
    Win,
    BorderMainSvg,
    NumberOrder,
  },
  data() {
    return {
      currentPage: "home",
    };
  },
  methods: {
    startGame() {
      this.currentPage = "game";
    },
    gameOver() {
      this.currentPage = "lose";
    },
    gameWon() {
      this.currentPage = "win";
    },
    backHome() {
      this.currentPage = "home";
    },
  },
};
</script>

<template>
  <BorderMainSvg><NumberOrder /> </BorderMainSvg>
  <Home v-if="currentPage === 'home'" @start-game="startGame" />
  <Game
    v-else-if="currentPage === 'game'"
    @game-over="gameOver"
    @game-won="gameWon"
  />
  <Lose
    v-else-if="currentPage === 'lose'"
    @back-home="backHome"
    @start-game="startGame"
  />
  <Win
    v-else-if="currentPage === 'win'"
    @back-home="backHome"
    @start-game="startGame"
  />
</template>
