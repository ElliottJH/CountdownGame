<template>
    <div id="app">
        <Start v-if="!gameState && answer == undefined" 
                :onStartClick="setGameState"/>
        <Game v-if="gameState" 
                :setGameState="setGameState"
                :setAnswer="setAnswer"
                :setLetters="setLetters"/>
        <Results v-if="!gameState && answer != undefined" 
                :restartGame="restartGame"
                 v-bind:answer="answer" 
                 v-bind:letters="letters"
                />        
    </div>
</template>

<script>
import Start from './components/Start.vue'
import Game from './components/Game.vue'
import Results from './components/Results.vue'

export default {
    name: 'app',
    data: () => ({
        gameState: false,
        answer: undefined,
        letters: undefined
    }),
    components: ({
        Start,
        Game, 
        Results
    }),
    methods: {
        setGameState: function (isRunning) {
            this.gameState = isRunning
        },
        setAnswer: function (answer){
            this.answer = answer
        },
        setLetters: function (letters){
            this.letters = letters
        },
        restartGame: function(){
            this.setAnswer(undefined)
            this.setLetters(undefined)
            this.setGameState(true)
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
  overflow-x:hidden;
}
#app > section{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    min-height: 100vh;
}
h1 {
  font-size: 3em;
  margin: .25em 0;
}
button {
  border: none;
  border-radius: 25px;
  padding: 15px 50px;
  cursor: pointer;
  color: white;
  font-size: 1.25em;
  font-weight: lighter;
  background-color: #3498db;
  box-shadow: 0 5px 20px rgba(0,0,0,.1), 0 5px 35px rgba(0,0,0,.3);
  transition: box-shadow .3s ease-in-out;
  outline: none;
  margin-bottom:50px;
}
h2 {
  color: gray;
  font-size: 1.3em
}
button:hover {
  box-shadow: 0 5px 20px rgba(0,0,0,.05), 0 5px 35px rgba(0,0,0,.05);
}
</style>