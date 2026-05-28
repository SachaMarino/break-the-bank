<script>
import BorderMainSvg from "@/components/svg/BorderMain.svg.vue";
import ButtonSvg from "@/components/svg/Button.svg.vue";
export default {
  components: {
    BorderMainSvg,
    ButtonSvg,
  },
};
</script>

<template>
  <BorderMainSvg>
    <h1 class="text-(--title) text-[clamp(2rem,3vw,2.5rem)] self-start">
      Break the bank
    </h1>
    <ButtonSvg>
      <button class="w-full h-full">Commencez</button>
    </ButtonSvg>
  </BorderMainSvg>
</template>
