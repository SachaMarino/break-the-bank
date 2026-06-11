<script>
import BorderMainSvg from "../svg/borderDesign/BorderMain.svg.vue";
import ButtonSvg from "../svg/borderDesign/Button.svg.vue";

export default {
  components: {
    ButtonSvg,
    BorderMainSvg,
  },
  data() {
    return {
      checkActive: "bg-(--primary) text-black",
      checkHover: "hover:bg-(--primary) hover:text-black",
      maxNumber: 9,
      currentNumber: 1,
      shuffleNumbers: [],
      foundNumbers: [],
      gameWon: false,
    };
  },
  methods: {
    startGame() {
      this.currentNumber = 1;
      this.foundNumbers = [];
      this.gameWon = false;

      const numbers = [];

      for (let i = 1; i <= this.maxNumber; i++) {
        numbers.push(i);
      }
      this.shuffleNumbers = numbers.sort(() => Math.random() - 0.5);
    },
    checkNumber(number) {
      if (number === this.currentNumber) {
        this.foundNumbers.push(number);
        if (this.currentNumber === this.maxNumber) {
          this.gameWon = true;
          this.$emit("success");
        } else {
          this.currentNumber++;
        }
      } else {
        alert("vie perdu, jeux suivant");
        this.$emit("fail");
      }
    },
  },
  mounted() {
    this.startGame();
  },
};
</script>
<template>
  <div class="w-full max-w-100">
    <h1 class="text-(--title) text-3xl">
      Cliquer les chiffres dans le bon ordre
    </h1>
    <div class="flex flex-wrap gap-2 justify-center items-center mt-20">
      <button
        v-for="number in shuffleNumbers"
        :key="number"
        class="w-full h-auto max-w-25 py-5 border border-(--primary) transition-all duration-100 text-2xl cursor-pointer"
        :class="[foundNumbers.includes(number) ? checkActive : checkHover]"
        @click="checkNumber(number)"
        :disabled="foundNumbers.includes(number)"
      >
        {{ foundNumbers.includes(number) ? "✓" : number }}
      </button>

      <div v-if="gameWon">
        <h2>Manche suivante</h2>
        <ButtonSvg>
          <button @click="startGame" class="py-3">Rejouer</button>
        </ButtonSvg>
      </div>
    </div>
  </div>
</template>

<style></style>
