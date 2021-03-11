<template>
  <div></div>
</template>

<script>
import getCharacterCards from "../characters";
import shuffle from "lodash.shuffle";

export default {
  data() {
    return {
      characters: shuffle(getCharacterCards()),
      guess1: null,
      guess2: null,
    };
  },
};
</script>

<style>
</style>