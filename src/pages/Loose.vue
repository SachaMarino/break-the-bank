<script>
import BorderContentSvg from "@/components/svg/borderDesign/BorderContent.svg.vue";
import BorderMainSvg from "@/components/svg/borderDesign/BorderMain.svg.vue";
import ButtonSvg from "@/components/svg/borderDesign/Button.svg.vue";
import TreasureSvg from "@/components/svg/Treasure.svg.vue";
import Warning from "@/components/svg/Warning.svg.vue";
import PoliceLight from "@/components/svg/PoliceLight.svg.vue";

export default {
  components: {
    BorderMainSvg,
    ButtonSvg,
    BorderContentSvg,
    TreasureSvg,
    Warning,
    PoliceLight,
  },
};
</script>

<template>
  <BorderMainSvg variant="loose" class="bg-(--shadow-error) flex">

    <div class="flex flex-col gap-5 w-full h-full justify-between">

      <div class="flex w-full  h-[20%] justify-between items-center p-20">
        <div class="flex gap-5 justify-start items-center">
          <Warning/>
          <h1 class="text-(--error) text-[clamp(3rem,3vw,2.5rem)] self-center">
            ERROR
          </h1>
        </div>
        <PoliceLight variant="loose"/>
      </div>
      
      <div class="flex w-full gap-5 h-[60%] justify-evenly mb-20 p-5">
        <div
          class="flex gap-5 w-[30%] h-full justify-center items-center"
        >
          <BorderContentSvg variant="loose">
            <h1 class="text-(--error) text-[clamp(3rem,3vw,2.5rem)] w-full">A̵̡̧̨̯͎̼̜̪̗̬̺͈͎͍͍͆̆̌̆̽̂̍̄̃̐͠ç̸̛̛̣̯̯͔͚̞͆̂́̑̍̑̄̊̈́̈́̽͠c̷̛̙̥̱͐́́̐ë̷̥̠̥͚̟̼͇̥̭̲́ͅͅś̴͚͖̲̯̠͚̹̥͉͕̣̮͖̬s̶̡̱̭͓̟̻͕̦̼̟̖̙̺̩̄̂̓͊͆̕ͅ ̵̡͊͋̔͒͋̒̈̈̈́̃́̕͠D̸̛͚̘̼͙̖̑͒̓̆́̏́̔̔͘͝͝ȩ̶̨̬̱̱̣͓̤͙̰͍̯͔̮̌̔͝n̶̢̺̣̥̹̻̝͈̬̟̖͔͙͉͙̬͑͊̉̆̾̆ĩ̵̛̠̳͋e̴̛͗̒̄̇̈́̃̽͗̑̔͋͘͘͜d̴̹͔̻̯͙̘͚̊̏̇́͛́̆̿̚̚ͅ</h1>
          </BorderContentSvg>
        </div>

        <div
          class="flex gap-5 w-[35%] h-full justify-center items-center"
        >
          <TreasureSvg variant="loose" />
        </div>

        <div class="flex flex-col w-[20%] gap-10 h-full justify-center items-end">
          <ButtonSvg variant="loose">
            <button class="w-full h-full cursor-pointer">Rejouer</button>
          </ButtonSvg>
          <ButtonSvg variant="loose">
            <button class="w-full h-full cursor-pointer">Accueil</button>
          </ButtonSvg>
        </div>
      </div>
    </div>
  </BorderMainSvg>
</template>
<style scoped>

</style>
