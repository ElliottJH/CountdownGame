<template>
    <div id="letters">
        <div>
            <input type="text" name="1" maxlength="1" disabled/>
            <input type="text" name="2" maxlength="1" disabled/>
            <input type="text" name="3" maxlength="1" disabled/>
            <input type="text" name="4" maxlength="1" disabled/>
            <input type="text" name="5" maxlength="1" disabled/>
            <input type="text" name="6" maxlength="1" disabled/>
            <input type="text" name="7" maxlength="1" disabled/>
            <input type="text" name="8" maxlength="1" disabled/>
        </div>
        <div>
            <button v-on:click="addConst">Continent</button>
            <button v-on:click="addVowel">Vowel</button>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Letters',
    data: () => ({
        used_letters: ['','','','','','','','']
    }),
    methods: {
        addConst: function(event) {
            const consts = ['q','w','r','t','y','p','s','d','f','g','h', 'j', 'k', 'l', 'z', 'x', 'v', 'b', 'n', 'm']
            this.addToLetters( consts[Math.floor(Math.random() * consts.length)] )  
        },
        addVowel: function(event) {
            const vowels = ['a', 'e', 'i', 'o', 'u']
            this.addToLetters( vowels[Math.floor(Math.random() * vowels.length)] )
        },
        addToLetters: function(letter){
            console.log(this.used_letters)
            for(let i = 0; i < this.used_letters.length; i++){
                if(this.used_letters[i] === ''){
                    this.used_letters[i] = letter
                    document.getElementsByName(i+1)[0].value = letter
                    return
                }
            }
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

</style>