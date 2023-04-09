<template>
  <div class="game-view">
    <card-flip
      v-for="(card, index) in arrayContext"
      :key="index"
      :imageUrl="`images/${card}.png`"
    />
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
  props: {
    arrayContext: {
      type: Array,
      default: () => [],
    },
  },
};
</script>

<style scoped>
.game-view {
  display: flex;
  flex-wrap: wrap;
  height: 100vh;
  margin: 1rem 25% 0 25%;
}
</style>
