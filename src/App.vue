<script>
import Home from "./pages/Home.vue";
import Game from "./pages/Game.vue";
import Lose from "./pages/Lose.vue";
export default {
  components: {
    Home,
    Game,
    Lose,
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
  },
};
</script>

<template>
  <Home v-if="currentPage === 'home'" @start-game="startGame" />
  <Game v-else-if="currentPage === 'game'" @game-over="gameOver" />
  <Lose v-else-if="currentPage === 'lose'" />
</template>
