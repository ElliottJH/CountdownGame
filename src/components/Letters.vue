<template>
    <div id="letters">
        <div>
            <input 
                type="text" 
                v-for="n in 8" 
                maxlength="1" 
                disabled 
                v-model="letters[n-1]" 
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
                maxlength="8" 
                id="wordAttempt"
                placeholder="enter your best answer" 
                @keydown="keyDown"
                v-model="attempt"
                />
        </div>
    </div>
</template>

<script>
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
        attempt: undefined
    }),
    methods: {
        addConst: function() {
            const consts = ['q','w','r','t','y','p','s','d','f','g','h', 'j', 'k', 'l', 'z', 'x', 'v', 'b', 'n', 'm']
            this.addToLetters( consts[Math.floor(Math.random() * consts.length)] )  
        },
        addVowel: function() {
            const vowels = ['a', 'e', 'i', 'o', 'u']
            this.addToLetters( vowels[Math.floor(Math.random() * vowels.length)] )
        },
        addToLetters: function(letter){
            const newLetters = this.letters.concat(letter)
            this.attempt = ''
            if(newLetters.length === 8) {
                this.letters = newLetters
                this.setClockRunning(true)
            }else if(newLetters.length < 8 ){
                this.letters = newLetters
            }
        },
        keyDown: function(event){
            if(event.key.length !== 1)
                return

            if( this.acceptLetter(event.key) )
                event.preventDefault();
        },
        acceptLetter: function(char){
            return (this.attempt.match(new RegExp(char, 'g')) || []).length >= (this.letters.toString().match(new RegExp(char, 'g')) || []).length
        }
    },
    watch: {
        attempt: function(){
            let remainingLetters = this.letters.concat()
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