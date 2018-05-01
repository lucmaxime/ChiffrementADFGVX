<template>
  <div id="app">
    <h1>Chiffrement ADFGVX</h1>
    <h2>Par Maxime Parret et Arnaud Plumez</h2>
    <Home/>
  </div>
</template>

<script>
import Home from './components/Home'

export default {
  name: 'App',
  components: {
    Home
  }
}
</script>

<style>
#app {
  background: #222;
  min-height: 100vh;
}
h1, h2 {
  margin: 0;
  text-align: center;
  color: white;
  font-size: 50px;
  padding-top: 10px;
}
h2 {
  font-size: 20px;
  padding-top: 2px;
  color: #666;
}
body, html {
  margin: 0;
  padding: 0;
  font-family: 'Roboto', sans-serif;
}
</style>
