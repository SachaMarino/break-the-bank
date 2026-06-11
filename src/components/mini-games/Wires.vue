<script>
export default {
    data() {
        return {
            wires: {
                red: false,
                blue: false,
                green: false,
                yellow: false,
            },
            shuffledWires: [],
            wireLines: {},
            draggingColor: null,
            draggingSide: null,
            start: null,
            mouse: null,
        };
    },
    mounted() {
        this.shuffleWires();
    },
    methods: {
        startDrag(color, side, event) {
            if (this.wires[color]) return;

            const startPoint = this.getElementCenter(event.currentTarget);

            this.draggingColor = color;
            this.draggingSide = side;
            this.start = startPoint;
            this.mouse = startPoint;
        },

        moveDrag(event) {
            if (!this.draggingColor) return;

            this.mouse = {
                x: event.clientX,
                y: event.clientY,
            };
        },

        stopDrag() {
            this.draggingColor = null;
            this.draggingSide = null;
            this.start = null;
            this.mouse = null;
        },

        connectWire(color, side, event) {
            const isSameColor = this.draggingColor === color;
            const isOppositeSide = this.draggingSide !== side;

            if (!this.draggingColor || !isSameColor || !isOppositeSide) {
                this.stopDrag();
                return;
            }

            this.wires[color] = true;
            this.wireLines[color] = {
                start: this.start,
                end: this.getElementCenter(event.currentTarget),
            };

            this.stopDrag();
        },

        getElementCenter(element) {
            const rect = element.getBoundingClientRect();

            return {
                x: rect.left + rect.width / 2,
                y: rect.top + rect.height / 2,
            };
        },

        shuffleWires() {
            const colors = Object.keys(this.wires);

            for (let i = colors.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [colors[i], colors[j]] = [colors[j], colors[i]];
            }

            this.shuffledWires = colors;
        },
    },
};
</script>

<template>
    <div
        class="container flex items-center justify-center p-8 flex-col gap-4"
        @mousemove="moveDrag"
        @mouseup="stopDrag"
    >
        <svg
            class="fixed inset-0 pointer-events-none z-50"
            width="100%"
            height="100%"
        >
            <line
                v-for="(line, color) in wireLines"
                :key="color"
                :x1="line.start.x"
                :y1="line.start.y"
                :x2="line.end.x"
                :y2="line.end.y"
                :stroke="color"
                stroke-width="6"
                stroke-linecap="round"
            />
            <line
                v-if="draggingColor && start && mouse"
                :x1="start.x"
                :y1="start.y"
                :x2="mouse.x"
                :y2="mouse.y"
                :stroke="draggingColor"
                stroke-width="6"
                stroke-linecap="round"
            />
        </svg>

        <div class="text-2xl font-bold">Wire Game</div>

        <div class="grid grid-cols-2 gap-x-24">
            <div class="grid gap-y-8">
                <div v-for="(dragState, color) in wires" :key="`left-${color}`">
                    <div
                        class="size-8 cursor-pointer rounded-full border-2 border-white shadow-md"
                        :style="{ backgroundColor: color }"
                        @mousedown="startDrag(color, 'left', $event)"
                        @mouseup.stop="connectWire(color, 'left', $event)"
                    ></div>
                </div>
            </div>

            <div class="grid gap-y-8">
                <div v-for="color in shuffledWires" :key="`right-${color}`">
                    <div
                        class="size-8 cursor-pointer rounded-full border-2 border-white shadow-md"
                        :style="{ backgroundColor: color }"
                        @mousedown="startDrag(color, 'right', $event)"
                        @mouseup.stop="connectWire(color, 'right', $event)"
                    ></div>
                </div>
            </div>
        </div>
    </div>
</template>
