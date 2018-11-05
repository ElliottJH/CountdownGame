<template>
    <div class="clock">
        <h1><span id="seconds">{{displaySeconds}}</span> : <span id="milliseconds">{{displayMilliseconds}}</span></h1>
    </div>
</template>

<script>
    export default {
        name: 'Clock',
        props: {
            milliseconds: Number,
            seconds: Number
        },
        data: () => ({
            displaySeconds: '00',
            displayMilliseconds: '00'
        }),
        watch: { 
            milliseconds: function() {
                this.displayMilliseconds = '' + this.milliseconds
                if(this.displayMilliseconds.length == 2){
                    this.displayMilliseconds = '0' + this.displayMilliseconds
                }else if(this.displayMilliseconds.length == 1){
                    this.displayMilliseconds = '00' + this.displayMilliseconds
                }
            },
            seconds: function() {
                this.displaySeconds = '' + this.seconds
                if(this.displaySeconds.length == 1){
                    this.displaySeconds = '0' + this.displaySeconds
                }else if(this.displaySeconds.length == 0){
                    this.displaySeconds = '00'
                }
            }
        }
    }
</script>

<style>

</style>