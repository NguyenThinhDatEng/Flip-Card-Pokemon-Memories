<template>
  <div class="game-view">
    <card-flip
      v-for="(card, index) in arrayContext"
      :key="index"
      :imageUrl="`images/${card}.png`"
      :cardContext="{ card, index }"
      ref="cardFlip"
      @flipped="checkRules"
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
            console.log("ok");
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
    };
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
