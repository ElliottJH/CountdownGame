<template>
    <section>
        <h1>Results</h1>
        <div id="answer">
            <h2>Your Attempt</h2>
            <p>{{message}}</p>
        </div>
        <div id="possibleResults">
            <h2>Top 10 words</h2>
            <p 
                type="text" 
                v-for="n in results.length" 
                maxlength="1" 
                disabled 
                :key="n"
                >
            {{results[n-1].word}}: {{results[n-1].meaning}}
            </p>    
        </div>
        <button @click="restartGame">Start a New Game</button>
    </section>
</template>

<script>
export default {
    name: 'Results',
    props: {
        restartGame: Function,
        answer: String,
        letters: Array,
    },
    data: () => ({
        message: 'Your word: you words meaning.',
        results: [
                    {word:'word one',meaning:'this is the example meaning for word one '}, 
                    {word:'word two',meaning:'this is the example meaning for word one '},
                    {word:'word one',meaning:'this is the example meaning for word one '}, 
                    {word:'word two',meaning:'this is the example meaning for word one '},
                    {word:'word one',meaning:'this is the example meaning for word one '}, 
                    {word:'word two',meaning:'this is the example meaning for word one '},
                    {word:'word one',meaning:'this is the example meaning for word one '}, 
                    {word:'word two',meaning:'this is the example meaning for word one '},
                    {word:'word one',meaning:'this is the example meaning for word one '}, 
                    {word:'word two',meaning:'this is the example meaning for word one this is the example meaning for word one this is the example meaning for word one '}
                ]
    }),
    methods: {
        getPossibleResults: function (){
            //call method with new results
        },
        isAnswerCorrect: function(){
            //calls to see if answer is correct
        }
    }
}
</script>

<style scoped>
section{
    width:66vw;
    margin:auto;
}

#answer p, #possibleResults p{
    padding-left:1em
}
#answer, #possibleResults{
    width:100%;
    padding-bottom: 0.5em;
}

</style>