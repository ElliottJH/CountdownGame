<template>
    <section>
        <h1>Results</h1>
        <div id="answer">
            <h2>Your Attempt</h2>
            <p>{{message}}</p>
        </div>
        <div id="possibleResults">
            <h2>Top 10 words</h2>
            <div 
                type="text"
                class="result" 
                v-for="n in results.length" 
                maxlength="1" 
                disabled 
                :key="n"
                >
                <p>{{results[n-1].Word}}: </p>
                <div class="meanings">
                    <p v-for="meaning in results[n-1].Meaning" :key="meaning">{{ meaning }}</p>
                </div>
            </div>
        </div>
        <button @click="restartGame">Start a New Game</button>
    </section>
</template>

<script>
import axios from 'axios'
export default {
    name: 'Results',
    props: {
        restartGame: Function,
        answer: String,
        letters: Array,
    },
    data: () => ({
        message: '',
        results: []
    }),
    methods: {
        getPossibleResults: function (){
            axios
            .get('http://localhost:8080/words?meaning=true&limit=10&letters='+this.letters.join(''))
            .then(response => {
                this.results = response.data.Words
                })
        },
        isAnswerCorrect: function(){
            if(this.answer != "" && this.answer != undefined){
                axios
                .get('http://localhost:8080/definition?word='+this.answer)
                .then(response => {
                    this.message = response.data.Word? response.data.Word + " : " + response.data.Meaning[0].toString() : this.answer + " : Is not a word"
                    })
            }else{
                 this.message = "No attempt given"
            }
        }
    },
    mounted(){
        this.isAnswerCorrect()
        this.getPossibleResults()
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
.result div{
    margin:5px;
}
.result p{
    display: inline;
}
.result>p:first-child{
    font-weight: bold;
}

</style>