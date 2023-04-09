<template>
  <game-level v-if="state == 'Choosing'" @selected="play" />
  <game-view v-if="state == 'Playing'" :arrayContext="settings.arrayContext" />
</template>

<script>
// Pages
import GameLevel from "@/pages/GameLevel.vue";
import GameView from "@/pages/GameView.vue";
// utils
import { shuffle } from "@/utils/array";

export default {
  name: "App",
  components: { GameLevel, GameView },
  props: {},
  // Functions
  methods: {
    play(config) {
      // Set up arrayContext
      let pokemonArr = Array.from(
        { length: config.numberOfCards / 2 },
        (_, i) => i + 1
      );
      pokemonArr = [...pokemonArr, ...pokemonArr];
      this.settings.arrayContext = shuffle(pokemonArr);
      console.log(this.settings.arrayContext);
      // Change state
      this.state = "Playing";
    },
  },
  data() {
    return {
      state: "Choosing",
      settings: {
        arrayContext: [],
      },
    };
  },
};
</script>
