<template>
    <section>
        <h2>Your Attempt</h2>
        <div id="answer">
            <p>{{ message[0] }}</p>
            <p>{{ message[1] }}</p>
            <p>{{ message[2] }}</p>
        </div>
        <h2>Top words</h2>
        <div id="possibleResults">
            <div 
                type="text"
                class="result" 
                v-for="n in results.length" 
                maxlength="1" 
                disabled 
                :key="n"
                >
                <p>{{ results[n-1].Word }}</p>
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
        message: ['No attempt given','-','0 Points'],
        results: []
    }),
    methods: {
        getPossibleResults: function (){
            axios
            .get('http://localhost:8080/words?meaning=true&limit=12&letters='+this.letters.join(''))
            .then(response => {
                this.results = response.data.Words
                })
        },
        isAnswerCorrect: function(){
            if(this.answer != "" && this.answer != undefined){
                axios
                .get('http://localhost:8080/definition?word='+this.answer)
                .then(response => {
                    this.message[0] = this.answer
                    this.message[1] = response.data.Word? response.data.Meaning[0].toString() : "You have entered an incorrect word"
                    this.message[2] = (response.data.Word? response.data.Word.length : 0) + " Points"
                    })
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
    padding-top: 50px;
}
section h2{
    align-self: baseline;
    color:black;
}
section button{
    margin-top:50px;
}
#answer{
    width: 100%;
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    align-items: stretch;
    align-content: center;
}
#answer p{
    flex-basis: auto;
    align-self: center;
}
#possibleResults{
    width: 100%;
    display: grid;
    grid-auto-flow:column;
    grid-template-rows: repeat(4, auto);
    grid-template-columns: repeat(3, Calc(100%/3));
    grid-gap: 10px;
}
.result>p{
    color: white;
    text-transform: capitalize;
    font-size: 20px;
    padding: 60px 20px;
    margin: 0;
    text-align: center;
}
.result p{
  background: #74b9ff;
}
.result:nth-child(odd) p{
  background: #74b9ff;
}
.result:nth-child(even) p{
  background: #82ccdd;
}
#answer p{
    display: inline-block;
    width: Calc(100%/3);
    text-align: center;
    padding: 30px 0px;
    color:white;
}

#answer p:first-child{
    background-color: #00b894;
    text-transform: capitalize;
}
#answer p:nth-child(2){
    background-color: #00cec9;
}
#answer p:last-child{
    background-color: #0984e3;
}

.meanings{
    display: none;
}
.result:hover .meanings{
    display: block;
}
.meanings p{
    padding: 2px;
    margin:0px;
}
.meanings p:nth-child(odd){
    color:#b2bec3;
    background-color: #2f3640;
}
.meanings p:nth-child(even){
    color:#b2bec3;
    background-color: #636e72;
}


</style>