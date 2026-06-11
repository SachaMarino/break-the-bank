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
    <BorderMainSvg variant="home">
        <div class="flex flex-col gap-5 w-full h-full justify-between">
            <h1 class="text-(--title) text-[clamp(2rem,3vw,2.5rem)] self-start">
                Break the bank
            </h1>
            <div
                class="flex flex-col md:flex-row md:justify-between gap-5 w-full h-full"
            >
                <BorderContentSvg variant="home" class="w-[20%] self-start">
                    <h1 class="self-start my-3 text-2xl">Bienvenue</h1>
                    <ul
                        class="self-start text-start flex flex-col gap-2 text-sm md:text-lg pr-4 lg:pr-5"
                    >
                        <li>
                            - Déverrouillez le coffre-fort en terminant tous les
                            mini-jeux.
                        </li>
                        <li>- Vous avez un temps limité pour chaque défi.</li>
                        <li>
                            - Vous disposez de 3 vies. Si le temps est écoulé
                            avant que vous ayez réussi, vous perdez une vie.
                        </li>
                        <li>
                            - Si vous perdez vos 3 vies, vous avez perdu et la
                            police intervient.
                        </li>
                    </ul>
                </BorderContentSvg>

                <div
                    class="flex w-[60%] flex-col gap-5 h-full justify-center items-center"
                >
                    <TreasureSvg variant="home" />
                    <ButtonSvg variant="home">
                        <button
                            class="w-full h-full cursor-pointer"
                            @click="$emit('start-game')"
                        >
                            Commencez
                        </button>
                    </ButtonSvg>
                </div>
            </div>
        </div>
    </BorderMainSvg>
</template>
<style scoped>
li {
    margin: 5px 2px;
    padding: 4px;
}
</style>
