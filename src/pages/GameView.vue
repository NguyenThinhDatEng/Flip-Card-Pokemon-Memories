<template>
  <div class="game-view">
    <card-flip />
  </div>
</template>

<script>
// Components
import CardFlip from "@/components/CardFlip.vue";
export default {
  name: "GameView",
  components: {
    CardFlip,
  },
};
</script>

<style scoped>
.game-view {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
</style>
