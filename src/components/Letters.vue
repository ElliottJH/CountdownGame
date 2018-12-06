<template>
    <div id="letters">
        <div>
            <input 
                type="text" 
                v-for="n in 9" 
                maxlength="1" 
                disabled 
                v-bind:value="letters[n-1] ? letters[n-1].toUpperCase() : ''" 
                :key="n"
                v-bind:class="[lettersChosen[n-1] === true ? 'used' : '']"
                />
        </div>
        <div>
            <button v-on:click="addConst">Consonant</button>
            <button v-on:click="addVowel">Vowel</button>
        </div>
        <div>
            <input 
                v-if="clockRunning" 
                maxlength="9" 
                id="wordAttempt"
                placeholder="enter your best answer" 
                @keydown="keyDown"
                v-model="attempt"
                />
        </div>
    </div>
</template>

<script>
import letterWeight from "../assets/letterWeight.json"

const getLetters = obj => {
    let letters = []
    Object.entries(obj).forEach(([key, value]) => {
         letters = letters.concat(Array(value).fill(key))
    })
    return letters
}

const generateRandomInt = (min, max) => {
    min = Math.ceil(min)
    return Math.floor(Math.random() * (Math.floor(max) - min)) + min;
}

export default {
    name: 'Letters',
    props: {
        setClockRunning: Function,
        setAnswer: Function,
        setLetters: Function,
        clockRunning: Boolean
    },
    data: () => ({
        lettersChosen: [],
        letters: [],
        attempt: undefined,
        consonant: getLetters(letterWeight.consonant),
        vowels: getLetters(letterWeight.vowels)
    }),
    methods: {
        addConst: function() {
            this.addLetter(this.consonant)
        },
        addVowel: function() {
            this.addLetter(this.vowels)
        },
        acceptLetter: function(char){
            return (this.attempt.match(new RegExp(char, 'g')) || []).length >= (this.letters.toString().match(new RegExp(char, 'g')) || []).length
        },
        addLetter: function(arr){
            if(this.letters.length === 9)
                return
            const index = generateRandomInt(0, arr.length)
            const letter = arr[index]
            arr.splice(index, 1)
            this.letters = this.letters.concat(letter)
            if(this.letters.length === 9) {
                this.attempt = ''
                this.setClockRunning(true)
            }
        },
        keyDown: function(event){
            if(event.key.length !== 1)
                return

            if(this.acceptLetter(event.key))
                event.preventDefault()
        }
    },
    watch: {
        attempt: function(){
            let remainingLetters = this.letters.slice(0)
            this.lettersChosen = []
                
            for(let i = 0; i <= remainingLetters.length; i++){
                let char = this.attempt[i]
                let index = remainingLetters.indexOf(char)
                if(index > -1){
                    remainingLetters[index] = undefined
                    this.lettersChosen[index] = true
                }
            }
            this.setAnswer(this.attempt)
        },
        letters: function(){
            this.setLetters(this.letters)
        }
    }
}
</script>

<style scoped>
input{
    width:3em;
    height:3em;
    padding: 0.5em;
    margin:0.5em;
    text-align: center;
    font-family: 'Open Sans', sans-serif;
    font-size: 1em;
    border-radius: 5px;
    border:none;
    background-color:ghostwhite;
}
.used{
    background-color: #2d3436;
    color: white;
}
#wordAttempt{
    width:100%;
}
button {
    border: none;
    width:Calc(50% - 2em);
    padding: 0.5em;
    margin:0.5em;
    border-radius: 5px;
    cursor: pointer;
    color: #2f3640;
    font-size: 1.25em;
    font-weight: lighter;
    background-color: #f1f2f6;
    box-shadow: 0 5px 20px rgba(0,0,0,.1), 0 5px 35px rgba(0,0,0,.3);
    transition: box-shadow .3s ease-in-out;
    outline: none;
    margin-bottom:50px;
}
button:hover{
    background-color: #dfe6e9;
}

#letters > div {
    display: flex;
    justify-content: center;
}

</style>