<template>
    <div class="clock">
        <h1><span id="seconds">{{displaySeconds}}</span><span id="colon"> : </span><span id="milliseconds">{{displayMilliseconds}}</span></h1>
    </div>
</template>

<script>
    export default {
        name: 'Clock',
        props: {
            milliseconds: Number,
            seconds: Number,
            clockStarted: Boolean
        },
        data: () => ({
            displaySeconds: '00',
            displayMilliseconds: '00'
        }),
        watch: { 
            milliseconds: function() {
                this.displayMilliseconds = this.numToDisplayString(this.milliseconds, true)
            },
            seconds: function() {
                this.displaySeconds = this.numToDisplayString(this.seconds, false)
            }
        },
        methods: {
            numToDisplayString: function(time, milli){
                time = time.toString()
                let startString = ''
                if(time.length == 2 && milli){
                    startString = '0'
                }else if(time.length == 1){
                    startString += '0'
                    if(milli)
                        startString += '0'
                }else if(time.length == 0){
                    startString = '00'
                }
                return startString + time
            }
        }
    }
</script>

<style scoped>
.clock h1{
    height: 20vh;
    color: white;
    font-size: 22vh;
    font-family: 'Open Sans', sans-serif;
    line-height: 20.4vh;
    display: flex;
    position: relative;
    overflow: hidden;
    -webkit-user-select: none; /* Safari */        
    -moz-user-select: none; /* Firefox */
    -ms-user-select: none; /* IE10+/Edge */
    user-select: none; /* Standard */
}
.black{
    color:black!important
}
#colon{
    font-size:15vh;
    line-height:17vh;
    padding:0 0.2em;
}
</style>