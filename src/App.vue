<template>
  <game-level v-if="state == 'Choosing'" @selected="state = 'Playing'" />
  <game-view v-if="state == 'Playing'" />
</template>

<script>
// Pages
import GameLevel from "@/pages/GameLevel.vue";
import GameView from "@/pages/GameView.vue";

export default {
  name: "App",
  components: { GameLevel, GameView },
  props: {},
  data() {
    return {
      state: "Choosing",
    };
  },
};
</script>
