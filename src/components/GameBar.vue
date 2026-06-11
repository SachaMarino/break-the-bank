<script>
import Timer from "./Timer.vue";

export default {
    props: {
        lives: {
            type: Number,
            required: true,
        },
        status: {
            type: String,
            required: true,
        },
    },
    components: {
        Timer,
    },
    emits: ["timeout"],
};
</script>

<template>
    <div class="h-10 p-4 w-full grid grid-cols-3 items-center justify-center">
        <div class="col-span-1 flex justify-start"></div>
        <div class="col-span-1 flex justify-center">
            <Timer @timeout="$emit('timeout')" v-if="status === 'playing'" />
        </div>
        <div class="col-span-1 flex justify-end">
            <span v-for="life in lives" :key="life">❤️</span>
        </div>
    </div>
</template>
