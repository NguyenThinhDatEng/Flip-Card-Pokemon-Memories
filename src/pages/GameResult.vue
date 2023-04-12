<template>
  <div class="result-screen">
    <h1>✨ Congratulations ✨</h1>
    <h3>{{ Math.round(timer / 1000) }} seconds</h3>
    <button @click="onStartAgain">Start Again</button>
  </div>
</template>
  
  <script>
export default {
  props: {
    timer: {
      type: Number,
      default: 0,
    },
  },
  emits: ["onStartAgain"],
  methods: {
    onStartAgain() {
      this.$emit("onStartAgain");
    },
  },
};
</script>
  
<style scoped>
.result-screen {
  height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

h1,
h3 {
  margin-bottom: 1rem;
}
</style>