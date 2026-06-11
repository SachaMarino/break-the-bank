<script>
import {
    createGameState,
    getCurrentMiniGame,
    loseLevel,
    winLevel,
    goToNextLevel,
} from "../lib/game-state";
import OrderNumber from "../components/mini-games/OrderNumber.vue";
import PlugWire from "../components/mini-games/PlugWire.vue";
import GameBar from "../components/GameBar.vue";

const miniGameComponents = {
    "order-number": OrderNumber,
    "plug-wire": PlugWire,
};

export default {
    components: {
        GameBar,
    },
    emits: ["game-over"],
    data() {
        return {
            state: createGameState(),
        };
    },
    computed: {
        currentMiniGame() {
            const currentMiniGameId = getCurrentMiniGame(this.state);

            if (!currentMiniGameId) {
                return null;
            }

            return miniGameComponents[currentMiniGameId];
        },
    },
    methods: {
        handleSuccess() {
            winLevel(this.state);
        },
        handleFail() {
            loseLevel(this.state);
            if (this.state.status === "lose") {
                this.$emit("game-over");
            }
        },
        handleNextLevel() {
            goToNextLevel(this.state);
        },
    },
};
</script>

<template>
    <GameBar
        :lives="state.lives"
        :status="state.status"
        :key="state.level"
        @timeout="handleFail"
    />
    <component
        v-if="state.status === 'playing'"
        :is="currentMiniGame"
        @success="handleSuccess"
        @fail="handleFail"
    />
    <div v-if="state.status === 'miniGameWon'">
        <div>Gagné 🎉</div>
        <button @click="handleNextLevel">Suivant</button>
    </div>
    <div v-if="state.status === 'miniGameLost'">
        <div>Perdu 💔</div>
        <button @click="handleNextLevel">Suivant</button>
    </div>
</template>
