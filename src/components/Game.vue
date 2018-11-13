<template>
    <section id="game" v-bind:class="[clockRunning === false ? 'stopped' :'']">
        <Clock :setClockRunning="setClockRunning" v-bind:clockRunning="clockRunning"/>
        <Letters :setClockRunning="setClockRunning" :setAnswer="setAnswer" v-bind:clockRunning="clockRunning"/>
    </section>
</template>

<script>
import Clock from './Clock.vue'
import Letters from './Letters.vue'

export default {
    name: 'Game',
    data: () => ({
        clockRunning: undefined,
        answer: undefined
    }),
    components: ({
        Clock,
        Letters
    }),
    methods: {
        setClockRunning: function (running) {
            this.clockRunning = running
        },
        setAnswer: function (answer){
            this.answer = answer
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