<template>
    <section>
        <h1>Countdown</h1>
        <h2>A game built in honor of the popular tv program Countdown</h2>
        <button @click="onStartClick">Start Countdown</button>
    </section>
</template>

<script>
export default {
    name: 'Start',
    props: {
        onStartClick: Function
    }
}
</script>

<style scoped>
h2 {
  margin-bottom:2em;
}
</style>