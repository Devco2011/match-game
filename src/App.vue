<template>
  <div id="app">
    <matching-game />
  </div>
</template>

<script>
import MatchingGame from "./components/MatchingGame";
export default {
  components: { MatchingGame },
  name: "App",
};
</script>

<style>
body {
  background-color: rgb(231, 133, 231);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
