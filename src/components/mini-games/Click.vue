<script>
import ButtonSvg from "../svg/borderDesign/Button.svg.vue";

export default {
  components: {
    ButtonSvg,
  },
  data() {
    return {
      clics: 0,
      goals: 25,
      win: false,
    };
  },
  methods: {
    increment() {
      if (this.win) return;

      this.clics++;

      if (this.clics >= this.goals) {
        this.win = true;
      }
    },
    restartGame() {
      this.clics = 0;
      this.win = false;
    },
  },
};
</script>
<template>
  <div class="flex flex-col gap-5 items-center mt-20 text-(--text-color)">
    <h1 class="text-(--title) text-3xl">Cliquez vite!</h1>
    <!-- Carré cliquable -->
    <div
      class="w-20 h-20 border-4 border-(--primary) hover:bg-(--primary) cursor-pointer transition-colors duration-200"
      @click="increment"
    ></div>

    <!-- Compteur -->
    <div class="text-3xl">
      <span v-if="!win">{{ clics }} / 25</span>
      <span v-else>🎉 Gagné !</span>
    </div>

    <!-- Bouton rejouer -->
    <ButtonSvg v-if="win">
      <button @click="restartGame" class="py-3">Rejouer</button>
    </ButtonSvg>
  </div>
</template>
