<template>
    <section class="start">
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.start {
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
  font-size: 1.3em
}
button:hover {
  box-shadow: 0 5px 20px rgba(0,0,0,.05), 0 5px 35px rgba(0,0,0,.05);
}
</style>