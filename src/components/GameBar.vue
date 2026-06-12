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
        score: {
            type: Number,
            required: true,
        }
    },
    components: {
        Timer,
    },
    emits: ["timeout"],
};
</script>

<template>
    <div class="h-10 p-4 w-full grid grid-cols-3 items-center justify-center">
        <div class="col-span-1 flex justify-start">
            <p class="text-(--title) text-5xl ml-15">{{ score }}</p>
        </div>
        <div class="col-span-1 flex justify-center">
            <Timer @timeout="$emit('timeout')" v-if="status === 'playing'" />
        </div>
        <div class="col-span-1 flex justify-end gap-3">
            <span v-for="life in lives" :key="life" class="w-10 h-10 border-2 border-(--primary) bg-(--primary)"></span>
            <span v-for="life in 3-lives" :key="life" class="w-10 h-10 border-2 border-(--primary) bg-(--secondary)"></span>
        </div>
    </div>
</template>
