<script>
export default {
  data() {
    return {
      heart: "❤️",
    };
  },
};
</script>
<template>
  <div class="flex">
    <span v-for="nbr in 3" :key="nbr">{{ heart }}</span>
  </div>
</template>
<style></style>
