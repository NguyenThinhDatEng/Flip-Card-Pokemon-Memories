<template>
  <div class="card" :style="{ height: height, width: width }">
    <div
      :class="[{ flipped: isFront }, { completed: isCompleted }, 'card__inner']"
      @click="onToggle"
    >
      <!-- front face -->
      <div class="card__face card__face--front">
        <div
          class="card__content"
          :style="{ backgroundSize: backgroundSize }"
        ></div>
      </div>
      <!-- back face -->
      <div class="card__face card__face--back">
        <div
          class="card__content"
          :style="{
            backgroundImage: `url(${require('@/assets/' + imageUrl)})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    imageUrl: {
      type: String,
      required: true,
    }, // url of image
    cardContext: {
      type: Object,
      default: () => {},
    }, // index and number of card
    numberOfRows: {
      type: Number,
      default: 4,
    }, // number of rows to show cards
  },

  created() {
    this.height = `calc((100vh - 16px * ${this.numberOfRows}) / ${this.numberOfRows} - 16px)`;
    this.width = `calc(((100vh - 16px * ${this.numberOfRows}) / ${this.numberOfRows} - 16px) * 3 / 4)`; // 3/4 height
    this.backgroundSize = `calc(((100vh - 16px * ${this.numberOfRows}) / ${this.numberOfRows} - 16px) * 3 / 4 / 3)`; // 1/3 width
  },

  methods: {
    /**
     * change isFront
     */
    onToggle() {
      if (this.isCompleted == false) {
        this.isFront = !this.isFront;
        this.$nextTick(() => {
          if (this.isFront === true) this.$emit("flipped", this.cardContext);
        });
      }
    },
  },

  data() {
    return {
      isFront: false,
      isCompleted: false,
      height: "",
      width: "",
      backgroundSize: "",
    };
  },
};
</script>

<style scoped>
.card {
  margin: 0 1rem 1rem 0;
}
.card__inner {
  position: relative;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  height: 100%;
  width: 100%;
}

.card__inner.flipped {
  transform: rotateY(180deg);
}

.card__inner.completed {
  cursor: default;
}

.card__face {
  position: absolute;
  padding: 1rem;
  border-radius: 8px;
  box-shadow: 0 3px 10px 3px rgb(0, 0, 0, 0.2);
  height: 100%;
  width: 100%;
  /* Ẩn mặt sau của element khi xoay */
  backface-visibility: hidden;
}

.card__face--front .card__content {
  background: url("@/assets/images/icon_back.png") no-repeat center center;
  width: 100%;
  height: 100%;
}

.card__face--back {
  background-color: var(--light);
  transform: rotateY(180deg);
}

.card__face--back .card__content {
  background-repeat: no-repeat;
  background-position: center center;
  background-size: contain;
  width: 100%;
  height: 100%;
}
</style>