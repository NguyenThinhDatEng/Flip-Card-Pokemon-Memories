<template>
  <div class="card">
    <div :class="[{ flipped: isFront }, 'card__inner']" @click="onToggle">
      <div class="card__face card__face--front">
        <div class="card__content">Front</div>
      </div>
      <div class="card__face card__face--back">
        <div class="card__content">Back</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    onToggle() {
      this.isFront = !this.isFront;
    },
  },

  data() {
    return {
      isFront: false,
    };
  },
};
</script>

<style scoped>
.card {
  width: 90px;
  height: 120px;
}
.card__inner {
  position: relative;
  transition: transform 1s;
  transform-style: preserve-3d;
  cursor: pointer;
  height: 100%;
}

.card__inner.flipped {
  transform: rotateY(180deg);
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

.card__face--back {
  background-color: var(--light);
  transform: rotateY(180deg);
}
</style>