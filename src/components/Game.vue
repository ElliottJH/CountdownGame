<template>
    <section id="game" v-bind:class="[clockRunning === false ? 'stopped' :'']">
        <div v-if="!gameEnded">
            <Clock :setClockRunning="setClockRunning" v-bind:clockRunning="clockRunning" v-bind:endGame="endGame"/>
            <Letters :setClockRunning="setClockRunning" :setAnswer="setAnswer" :setLetters="setLetters" v-bind:clockRunning="clockRunning"/>
        </div>
        <div v-if="gameEnded">
            <Results v-bind:restartGame="restartGame" v-bind:answer="answer" v-bind:letters="letters" />
        </div>
    </section>
</template>

<script>
import Clock from './Clock.vue'
import Letters from './Letters.vue'
import Results from './Results.vue'

export default {
    name: 'Game',
    data: () => ({
        clockRunning: undefined,
        answer: undefined,
        letters: undefined, 
        gameEnded: undefined
    }),
    components: ({
        Clock,
        Letters,
        Results
    }),
    methods: {
        setClockRunning: function (running) {
            this.clockRunning = running
        },
        setAnswer: function (answer){
            this.answer = answer
        },
        setLetters: function (letters){
            this.letters = letters
        },
        endGame: function (){
            this.gameEnded = true
        },
        restartGame: function(){
            this.clockRunning = undefined
            this.answer = undefined
            this.letters = undefined
            this.gameEnded = undefined
        }
    }
}
</script>

<style scoped>
#game {
    background-color:#44bd32
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
    margin-bottom:2em;
}
button:hover {
    box-shadow: 0 5px 20px rgba(0,0,0,.05), 0 5px 35px rgba(0,0,0,.05);
}

.stopped{
    background-color:#EA2027!important;
}
</style>