<script>
import BorderContentSvg from "@/components/svg/borderDesign/BorderContent.svg.vue";
import BorderMainSvg from "@/components/svg/borderDesign/BorderMain.svg.vue";
import ButtonSvg from "@/components/svg/borderDesign/Button.svg.vue";
import TreasureSvg from "@/components/svg/Treasure.svg.vue";

export default {
  components: {
    BorderMainSvg,
    ButtonSvg,
    BorderContentSvg,
    TreasureSvg,
  },
};
</script>

<template>
  <BorderMainSvg>
    <h1 class="text-(--title) text-[clamp(2rem,3vw,2.5rem)] self-start">
      Break the bank
    </h1>
    <div
      class="flex flex-col md:flex-row md:justify-between gap-5 w-full h-full"
    >
      <BorderContentSvg class="w-[20%] self-start">
        <h1 class="self-start">Hello</h1>
      </BorderContentSvg>

      <div
        class="flex w-[80%] flex-col gap-5 h-full justify-center items-center"
      >
        <TreasureSvg />
        <ButtonSvg>
          <button class="w-full h-full">Commencez</button>
        </ButtonSvg>
      </div>
    </div>
  </BorderMainSvg>
</template>
