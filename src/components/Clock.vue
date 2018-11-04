<template>
    <div class="clock">
        <canvas id="canvas" width="400" height="400" style="background-color:#333"></canvas>
    </div>
</template>

<script>
    export default {
        name: 'Clock',
        props: {
            startClock: Function,
            endClock: Function
        }
    }
</script>

<style>

</style>