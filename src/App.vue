<script>
import Defusing from "./components/mini-games/Defusing.vue";
import OrderNumber from "./components/mini-games/OrderNumber.vue";
import Wires from "./components/mini-games/Wires.vue";
import Home from "./pages/Home.vue";
export default {
  components: {
    Home,
    Defusing,
  },
};
</script>

<template>
  <Home />
  <Defusing />
</template>
