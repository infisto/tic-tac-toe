<template>
  <div id="app">
    <TicTacToe></TicTacToe>
  </div>
</template>

<script>
import TicTacToe from "@/components/TicTacToe";
export default {
  name: "App",
  components: {
    TicTacToe
  }
};
</script>

<style>
*, *:after, *:before {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
html, body {
  height: 100%;
}
#app {
  font-family: "Acquest Script", sans-serif, sans-serif;
  font-size: 25px;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #14bdac;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
