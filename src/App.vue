<script>
import Click from "./components/mini-games/Click.vue";
import Defusing from "./components/mini-games/Defusing.vue";
import Home from "./pages/Home.vue";
export default {
  components: {
    Home,
    Defusing,
    Click,
  },
};
</script>

<template>
  <Home />
  <Click />
</template>
