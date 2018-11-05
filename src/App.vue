<template>
    <div id="app">
        <Start v-if="!gameStarted" :onStartClick="startGame"/>
        <Game v-if="gameStarted" />
    </div>
</template>

<script>
import Start from './components/Start.vue'
import Game from './components/Game.vue'

export default {
    name: 'app',
    data: () => ({
        gameStarted: false
    }),
    components: ({
        Start,
        Game
    }),
    methods: {
        startGame: function () {
            this.gameStarted = true
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    -webkit-user-select: none; /* Safari */        
    -moz-user-select: none; /* Firefox */
    -ms-user-select: none; /* IE10+/Edge */
    user-select: none; /* Standard */
}

body, html{
  height: 100vh;
  width: 100vw;
  margin: 0;
}

#app {
  height:100%;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-template-rows: repeat(3, 1fr);
  align-items: center;
  justify-content: center;
}
.running{
    background-color:#44bd32
}
.stopped{
    background-color:#EA2027
}
</style>