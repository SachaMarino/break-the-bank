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
      progress : 0,
      isComplete: false,
      intervalId: null,
      speed: 1,
      gameWon:false,
    };
  },
  methods: {
    startFilling() {
      if (this.intervalId || this.isComplete) return

      this.intervalId = setInterval(() => {
        if (this.progress < 100) {
          this.progress += this.speed;
        } else {
          clearInterval(this.intervalId);
          this.intervalId = null;
          this.isComplete = true;
          this.stopFilling();
        }
      }, 30)
    },
    stopFilling(){
      if (this.isComplete){
        this.gameWon = true;
      }
      
      clearInterval(this.intervalId)
      this.intervalId = null;
    },
  },
};
</script>

<template>

  <BorderMainSvg>
    <div class="w-full max-w-100 flex flex-col gap-15">
      <h1 class="text-(--title) text-3xl">
        Remplire la jaune en maintenant le boutton
      </h1>
      
      <div class="flex flex-col gap-3">
        <div class="w-full h-8 bg-(--secondary) border-2 border-(--primary) overflow-hidden mb-4">
          <div 
            class="h-full bg-(--primary) transition-all duration-100 ease-linear"
            :style="{ width: `${progress}%` }"
          ></div>
        </div>
        
        <ButtonSvg>
          <button
            @mousedown="startFilling()"
            @mouseup="stopFilling()"
            @mouseleave="stopFilling()"
            @touchstart="startFilling()"
            @touchend="stopFilling()"
            class="px-6 py-3 transition-colors select-none active:scale-95 duration-150 w-100"
          >
            Maintenir enfoncé
          </button>
        </ButtonSvg>
      </div>
    </div>
  </BorderMainSvg>
</template>