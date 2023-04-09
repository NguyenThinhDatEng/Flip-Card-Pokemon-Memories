<template>
  <div class="game-level">
    <h1>POKE MEMORIES</h1>
    <h3>Select mode to start game</h3>
    <div class="levels">
      <button @click="onClickLevel(4 * 4)">
        <p>4x4</p>
        <p>Easy</p>
      </button>
      <button @click="onClickLevel(6 * 6)">
        <p>6x6</p>
        <p>Normal</p>
      </button>
      <button @click="onClickLevel(8 * 8)">
        <p>8x8</p>
        <p>Hard</p>
      </button>
      <button @click="onClickLevel(10 * 10)">
        <p>10x10</p>
        <p>Super Hard</p>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "GameLevel",
  emits: ["selected"],
  methods: {
    onClickLevel(numberOfCards) {
      this.$emit("selected", { numberOfCards });
    },
  },
};
</script>

<style>
.game-level {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  height: 100vh;
}

.game-level .levels {
  display: inline-flex;
}

.levels + .levels {
  margin-left: 8px;
}

.game-level .levels button {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  width: 100px;
  height: 200px;
}
</style>
