<template>
  <div>
    <h1 v-if="foundAllMatches">Great job! You found all the Ponies!</h1>
    <h1 v-else>Find the Matching Ponies</h1>
    <div class="game-board">
      <div v-for="character in characters" :key="character.id" class="cell">
        <game-card
          :character="character"
          :guess1="guess1"
          :guess2="guess2"
          @select="handleCardClick"
        />
      </div>
    </div>
  </div>
</template>

<script>
import getCharacterCards from "../characters";
import GameCard from "./GameCard";
import shuffle from "lodash.shuffle";

export default {
  components: { GameCard },
  data() {
    return {
      characters: shuffle(getCharacterCards()),
      guess1: null,
      guess2: null,
    };
  },
  methods: {
    handleCardClick(characterClicked) {
      console.log(characterClicked);
      if (this.guess1 && this.guess2) return;

      if (this.guess1 === characterClicked) return;

      if (this.guess1 === null) {
        this.guess1 = characterClicked;
        return;
      }
      this.guess2 = characterClicked;

      const [character1, character2] = this.getMatchingCharacters(
        characterClicked.name
      );

      if (this.guess1.name === this.guess2.name) {
        character1.foundMatch = true;
        character2.foundMatch = true;
        this.guess1 = null;
        this.guess2 = null;
      } else {
        setTimeout(() => {
          this.guess1 = null;
          this.guess2 = null;
        }, 1500);
      }
    },
    getMatchingCharacters(name) {
      return this.characters.filter((c) => c.name === name);
    },
  },
  computed: {
    foundAllMatches() {
      return this.characters.every((c) => c.foundMatch);
    },
  },
};
</script>

<style scoped>
h1 {
  color: #333;
}
.game-board {
  display: flex;
  flex-wrap: wrap;
  align-items: space-between;
  justify-content: center;
}
.cell {
  padding: 10px;
}
</style>