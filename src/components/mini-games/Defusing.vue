<script>
import ButtonSvg from "../svg/borderDesign/Button.svg.vue";

export default {
  components: {
    ButtonSvg,
  },
  data() {
    return {
      wireCount: 6,
      bombWires: 1,
      wires: [],
      gameOver: false,
      message: "",
      cutSafeWires: 0,
      winMessageDesign: "text-(--success)",
      loseMessageDesign: "text-(--error)",
    };
  },
  mounted() {
    this.initGame();
  },
  methods: {
    initGame() {
      this.gameOver = false;
      this.message = "";
      this.cutSafeWires = 0;

      // Wire init
      this.wires = Array(this.wireCount)
        .fill()
        .map(() => ({
          type: "safe",
          cut: false,
        }));

      // red wire random
      let bombsPlaced = 0;
      while (bombsPlaced < this.bombWires) {
        const idx = Math.floor(Math.random() * this.wireCount);
        if (this.wires[idx].type !== "bomb") {
          this.wires[idx].type = "bomb";
          bombsPlaced++;
        }
      }
    },
    cutWire(index) {
      if (this.gameOver || this.wires[index].cut) return;

      this.wires[index].cut = true;

      if (this.wires[index].type === "bomb") {
        this.message = " ❌Perdu! Mauvais fil coupé!";
        this.gameOver = true;
        return;
      }

      this.cutSafeWires++;

      if (this.cutSafeWires === this.wireCount - this.bombWires) {
        this.message = "✅Bombe désamorcée !";
        this.gameOver = true;
      }
    },
    restartGame() {
      this.initGame();
    },
    wireClass(wire) {
      if (!wire.cut) return "bg-gray-500 hover:bg-gray-400";
      return wire.type === "bomb"
        ? "bg-(--error) shadow-[0_0_10px_red] cursor-default"
        : "bg-green-400 shadow-[0_0_10px_#00ff00] cursor-default";
    },
  },
};
</script>
<template>
  <div class="flex flex-col items-center justify-center">
    <h1 class="text-(--title) text-3xl">
      Coupe les bons fils pour désamorcer la bombe !
    </h1>

    <div class="mt-8 w-80 border-2 border-(--primary) rounded-xl p-6 m-5">
      <div class="flex flex-col items-center gap-4">
        <div
          v-for="(wire, index) in wires"
          :key="index"
          @click="cutWire(index)"
          class="h-3 w-full rounded-full transition-all duration-300 cursor-pointer"
          :class="wireClass(wire)"
        ></div>
      </div>

      <p
        v-if="message"
        class="mt-6 text-center font-bold text-lg"
        :class="message.includes('✅') ? winMessageDesign : loseMessageDesign"
      >
        {{ message }}
      </p>
    </div>
    <ButtonSvg>
      <button @click="restartGame" class="py-3">Rejouer</button>
    </ButtonSvg>
  </div>
</template>
