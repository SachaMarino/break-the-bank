<script>
import ButtonSvg from "../svg/borderDesign/Button.svg.vue";

export default {
  components: {
    ButtonSvg,
  },
  data() {
    return {
      wireCount: 7,
      bombWires: 3,
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
        this.$emit("fail");
        return;
      }

      this.cutSafeWires++;

      if (this.cutSafeWires === this.wireCount - this.bombWires) {
        this.message = "✅Bombe désamorcée !";
        this.$emit("success");
      }
    },
    restartGame() {
      this.initGame();
    },
    wireClass(wire) {
      if (wire.type === "bomb") {
        return "hover:bg-(--error) hover:shadow-[0_0_10px_red] cursor-default";
      } else {
        if (wire.cut) {
          return "bg-green-400 shadow-[0_0_10px_#00ff00]";
        } else {
          return "hover:bg-green-400 hover:shadow-[0_0_10px_#00ff00] cursor-default";
        }
      }
    },
  },
};
</script>
<template>
  <div class="flex flex-col items-center">
    <h1 class="text-(--title) text-3xl">
      Coupe les bons fils pour désamorcer la bombe !
    </h1>

    <div
      class="mt-8 w-full max-w-100 border-2 border-(--primary) rounded-xl p-6 m-5"
    >
      <div class="flex flex-col items-center gap-6">
        <div
          v-for="(wire, index) in wires"
          :key="index"
          @click="cutWire(index)"
          class="h-5 w-full rounded-full transition-all duration-300 cursor-pointer bg-gray-500"
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
  </div>
</template>
