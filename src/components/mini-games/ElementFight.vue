<script>
import Fire from "../svg/Fire.vue";
import Ice from "../svg/Ice.vue";
import Water from "../svg/Water.vue";

export default {
  components: {
    Fire,
    Ice,
    Water,
  },
  data() {
    return {
      playerChoice: null,
      cpuChoice: null,
      message: "",
      locked: false,
    };
  },

  mounted() {
    this.newRound();
  },

  methods: {
    newRound() {
      const choices = ["water", "fire", "ice"];
      this.cpuChoice = choices[Math.floor(Math.random() * 3)];
    },

    play(choice) {
      if (this.locked) return;

      this.locked = true;
      this.playerChoice = choice;
      this.message = "";

      const result = this.getResult(choice, this.cpuChoice);
      this.message = result;

      if (result === "🤝 Égalité") {
        setTimeout(() => {
          this.playerChoice = null;
          this.message = "";
          this.newRound();
          this.locked = false;
        }, 1000);
        return;
      }

      this.locked = false;
      this.newRound();
    },

    getResult(player, cpu) {
      if (player === cpu) return "🤝 Égalité";

      if (
        (player === "fire" && cpu === "ice") ||
        (player === "ice" && cpu === "water") ||
        (player === "water" && cpu === "fire")
      ) {
        return this.$emit("success");
      }

      return this.$emit("fail");
    },

    format(choice) {
      if (choice === "water") return "💧 Eau";
      if (choice === "fire") return "🔥 Feu";
      if (choice === "ice") return "🧊 Glace";
    },

    reset() {
      this.playerChoice = null;
      this.message = "";
      this.locked = false;
      this.newRound();
    },
  },
};
</script>
<template>
  <div>
    <h1 class="text-(--title) text-2xl md:text-3xl pb-5">
      Eau / Feu / Glace 🔥💧🧊
    </h1>

    <div class="flex justify-center gap-2 w-full">
      <button
        @click="play('water')"
        :disabled="locked"
        class="flex flex-col justify-center items-center w-full"
      >
        <Water class="h-10 w-10" /><span>Eau</span>
      </button>
      <button
        @click="play('fire')"
        :disabled="locked"
        class="flex flex-col justify-center items-center w-full"
      >
        <Fire class="h-10 w-10" /> <span>Feu</span>
      </button>
      <button
        @click="play('ice')"
        :disabled="locked"
        class="flex flex-col justify-center items-center w-full"
      >
        <Ice class="h-10 w-10" /><span>Glace</span>
      </button>
    </div>

    <div class="my-4 text-md md:text-2xl">
      <p>AI : {{ format(cpuChoice) }}</p>
      <p v-if="playerChoice">Toi : {{ format(playerChoice) }}</p>
      <h3>{{ message }}</h3>
    </div>
  </div>
</template>

<style scoped>
button {
  border: 2px solid var(--primary);
  font-size: clamp(14px, 3vw, 18px);
  padding: 0.5rem;
  cursor: pointer;
}
button:hover {
  background-color: var(--primary);
  color: black;
  font-weight: 600;
}
</style>
