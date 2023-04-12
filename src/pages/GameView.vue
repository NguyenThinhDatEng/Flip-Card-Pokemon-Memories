<template>
  <div class="match-screen">
    <div class="game-view" :style="{ width: width }">
      <card-flip
        v-for="(card, index) in arrayContext"
        :key="index"
        :imageUrl="`images/${card}.png`"
        :cardContext="{ card, index }"
        :numberOfRows="numberOfRows"
        ref="cardFlip"
        @flipped="checkRules"
      />
    </div>
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
  emits: ["completedMatch"],
  props: {
    arrayContext: {
      type: Array,
      default: () => [],
    },
  },

  computed: {
    numberOfRows: function () {
      return Math.sqrt(this.arrayContext.length);
    },
  },

  created() {
    this.width = `calc(((100vh - 16px * ${this.numberOfRows}) / ${this.numberOfRows} - 16px) * 3 / 4 * ${this.numberOfRows} + 16px * ${this.numberOfRows})`;
  },

  // methods
  methods: {
    /**
     *
     * @param {Object} cardContext include index and card number
     */
    checkRules: function (cardContext) {
      if (this.flippedCards.length === 2) {
        return;
      }

      this.flippedCards.push(cardContext);

      const arrTmp = this.flippedCards;
      if (this.flippedCards.length === 2) {
        if (this.flippedCards[0].card === this.flippedCards[1].card) {
          this.$refs.cardFlip[arrTmp[0].index].isCompleted = true;
          this.$refs.cardFlip[arrTmp[1].index].isCompleted = true;
          if (this.isEndGame()) {
            this.$emit("completedMatch");
          }
          this.flippedCards = [];
        } else {
          setTimeout(() => {
            this.$refs.cardFlip[arrTmp[0].index].isFront = false;
            this.$refs.cardFlip[arrTmp[1].index].isFront = false;
          }, 700);
          this.flippedCards = [];
        }
      }
    },

    isEndGame: function () {
      const numberOfCompletedCards = this.$refs.cardFlip.filter(
        (item) => item.isCompleted == true
      ).length;
      console.log(numberOfCompletedCards);
      return numberOfCompletedCards === this.arrayContext.length;
    },
  },

  data() {
    return {
      flippedCards: [],
      height: "",
      width: "",
    };
  },
};
</script>

<style scoped>
.match-screen {
  display: flex;
  justify-content: center;
  background-color: var(--dark);
  height: 100vh;
}
.game-view {
  display: flex;
  flex-wrap: wrap;
  margin: 2rem auto;
}
</style>
