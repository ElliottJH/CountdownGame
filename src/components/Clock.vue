<template>
    <div class="clock">
        <h1><span id="seconds">{{numToDisplayString(seconds, false)}}</span><span id="colon"> : </span><span id="milliseconds">{{numToDisplayString(milliseconds, true)}}</span></h1>
    </div>
</template>

<script>
    export default {
        name: 'Clock',
        props: {
            clockRunning: Boolean,
            setClockRunning: Function
        },
        data: () => ({
            seconds: 30,
            milliseconds: 0
        }),
        methods: {
            numToDisplayString: function(time, milli){
                // REFACTOR THIS UGLYNESSSSSSSSSSSSSZSZSDAS11!!!111
                // ^^^ rude
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
            },
            increaseTime: function(startTime) { 
                setTimeout(() => {
                    if(this.seconds <= 0 ){
                        this.milliseconds = 0
                        this.setClockRunning(false)
                        return
                    }

                    let elapsedTime = new Date(Date.now() - startTime)
                    this.seconds = 29 - elapsedTime.getSeconds()
                    this.milliseconds = 1000 - elapsedTime.getMilliseconds()
                    this.increaseTime(startTime)
                }, 20)
            }
        },
        watch: {
            clockRunning: function(){
                if (this.clockRunning) {
                    this.increaseTime(new Date())
                }
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