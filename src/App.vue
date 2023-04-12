<template>
  <game-level v-if="state == 'Choosing'" @selected="play" />
  <game-view
    v-if="state == 'Playing'"
    :arrayContext="settings.arrayContext"
    @completedMatch="completedMatch"
  />
  <game-result
    v-if="state == 'Result'"
    :timer="timer"
    @onStartAgain="onStartAgain"
  />
</template>

<script>
// Pages
import GameLevel from "@/pages/GameLevel.vue";
import GameView from "@/pages/GameView.vue";
import GameResult from "./pages/GameResult.vue";
// utils
import { shuffle } from "@/utils/array";

export default {
  name: "App",
  components: { GameLevel, GameView, GameResult },
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
      // Change state
      this.state = "Playing";
      // update setting
      this.settings.startAt = new Date().getTime();
    },

    completedMatch: function () {
      // get total of time to complete match
      this.timer = new Date().getTime() - this.settings.startAt;
      this.state = "Result";
    },

    onStartAgain: function () {
      this.state = "Choosing";
    },
  },
  data() {
    return {
      state: "Choosing",
      settings: {
        arrayContext: [],
        startAt: null,
      },
      timer: 0,
    };
  },
};
</script>
