<template>
  <div class="card" :class="{ flipped: isShown }">
    <div class="card-inner" @click="handleClick">
      <div class="back-side">
        <img src="@/assets/images/star.png" alt="hidden card" />
      </div>
      <div class="character-side">
        <img
          :src="require(`@/assets/images/` + character.image)"
          :alt="character.name"
          :title="character.name"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["character", "guess1", "guess2"],
  methods: {
    handleClick() {
      this.$emit("select", this.character);
    },
  },
  computed: {
    isShown() {
      return (
        this.character.foundMatch ||
        this.character === this.guess1 ||
        this.character === this.guess2
      );
    },
  },
};
</script>

<style scoped>
img {
  height: 120px;
}
.card {
  background-color: transparent;
  width: 120px;
  height: 120px;
  perspective: 1000px;
  margin-top: 20px;
}
.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
}
.flipped .card-inner {
  transform: rotateY(180deg);
}
.back-side,
.character-side {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
}
.back-side {
  background-color: transparent;
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: auto 60px;
}
.character-side {
  background-color: transparent;
  color: black;
  transform: rotateY(180deg);
}
</style>