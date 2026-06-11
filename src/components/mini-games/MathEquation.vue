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
      keyboard: [1,2,3,4,5,6,7,8,9,'✖',0,'✓'],
      firstNb: 1,
      secNb: 1,
      response: '',
      gameWon:false,
    };
  },
  methods: {
    startGame() {
      this.gameWon = false;
      this.response = '';
      this.firstNb = Math.floor(Math.random() * 9) + 1;
      this.secNb = Math.floor(Math.random() * 9) + 1;
    },
    handleKey(key){
      switch (key){
        case '✖':
          this.response = "";
          break;
        case '✓':
          this.submitResponse();
          break;
        default:
          this.response += key;
          break;
      }
    },
    submitResponse(){
      if(Number(this.response) === (this.firstNb * this.secNb)){
        console.log('true');
        this.gameWon = true;
      }else{
        console.log('false');

      }
    }
  },
  mounted() {
    this.startGame();
  },
};
</script>
<template>
  <BorderMainSvg>
    <div class="w-full max-w-100 flex flex-col gap-5">
      <h1 class="text-(--title) text-3xl">
        Résoudre ce probleme de math
      </h1>
      <p class="text-(--title) text-5xl w-fit m-auto px-5 py-2 border border-(--primary)"> {{ firstNb }} X {{ secNb }}</p>
      <input type="number" v-model="response" @keyup.enter="submitResponse()" min="0" name="response" id="response" class="text-(--title) text-3xl max-w-80 m-auto px-5 py-2 border border-(--primary)">
      <div class="flex flex-wrap gap-2 justify-center items-center">
        <button
          v-for="key in keyboard"
          :key="key"
          class="w-full h-auto max-w-25 py-5 border border-(--primary) hover:bg-(--primary) hover:text-black transition-all duration-100 text-2xl cursor-pointer"
          @click="handleKey(key)"
        >
        {{ key }}
        </button>

        <div v-if="gameWon">
          <h2>Manche suivante</h2>
          <ButtonSvg>
            <button @click="startGame" class="py-3">Rejouer</button>
          </ButtonSvg>
        </div>
      </div>
    </div>
  </BorderMainSvg>
</template>

<style></style>
