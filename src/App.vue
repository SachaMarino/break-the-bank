<script>
import OrderNumber from "./components/mini-games/OrderNumber.vue";
import BorderMainSvg from "./components/svg/borderDesign/BorderMain.svg.vue";
import Home from "./pages/Home.vue";
export default {
  components: {
    Home,
    OrderNumber,
    BorderMainSvg,
  },
};
</script>

<template>
  <Home />
  <BorderMainSvg>
    <OrderNumber />
  </BorderMainSvg>
</template>
