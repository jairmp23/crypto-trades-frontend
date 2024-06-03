<template>
  <div id="app">
    <h1>Crypto Trades</h1>
    <TradeList />
  </div>
</template>

<script setup>
import TradeList from './components/TradeList.vue';
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
