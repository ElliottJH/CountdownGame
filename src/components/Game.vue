<template>
    <section class="game">
        <Clock v-bind:milliseconds="milliseconds" v-bind:seconds="seconds" v-bind:startClock="startClock"/>
        <Letters />
    </section>
</template>

<script>
import Clock from './Clock.vue'
import Letters from './Letters.vue'

export default {
    name: 'Game',
    data: () => ({
        startClock: false,
        seconds: 0,
        milliseconds: 0
    }),
    components: ({
        Clock,
        Letters
    }),
    mounted: function(){
        document.getElementById('app').classList.add('running')
        document.getElementById('app').classList.remove('stopped')
        let increaseTime = (start_time) => {
            setTimeout(() => {
                if(this.seconds >= 30){
                    this.milliseconds = 0
                document.getElementById('app').classList.remove('running')
                document.getElementById('app').classList.add('stopped')
                    return
                }
                let elapsed_time = Date.now() - start_time
                this.seconds = Math.floor(elapsed_time/1000)
                this.milliseconds = elapsed_time - this.seconds*1000
                increaseTime(start_time)
            }, 20)
        }
        increaseTime(Date.now())
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .game {
    grid-row: 2;
    grid-column: 2;
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
</style>