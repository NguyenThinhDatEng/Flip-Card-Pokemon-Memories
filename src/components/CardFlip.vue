<template>
  <div class="card">
    <div class="card__inner">
      <div class="card__face card__face--back" v-if="isFront"></div>
      <div class="card__face card__face--front" v-else></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isFront: true,
    };
  },
};
</script>

<style scoped>
.card__face {
  width: 100px;
  height: 100px;
  background-color: #000;
}
</style>