<template lang="html">
<div>
  <h1>Guess Who!</h1>
  <h2 v-if="characterFound">Congratulations it was {{this.mysteryCharacter.name}}</h2>
  <list-characters
  v-if="this.characters"
  :characters="this.characters"></list-characters>

  <select-choices
  v-if="this.choices"
  :choices="this.choices"
  ></select-choices>
</div>
</template>

<script>
import ListCharacters from "./components/ListCharacters.vue"
import SelectChoices from "./components/SelectChoices.vue"
import {eventBus} from "./main.js"


export default {
  name: 'app',
  data() {
    return {
      characters: null,
      choices: null,
      selectedCharacter: null,
      mysteryCharacter: null,
      previousSelectedCharacters: [],
      previousChoices: [],
      characterFound: false

    }
  },


  mounted() {
    this.getCharacters();
    this.getChoices();

    eventBus.$on('character-selected', (characterSelect) =>{
      this.selectedCharacter = characterSelect
    });
  },
  watch: {
    selectedCharacter: function(){
      this.guessCharacter()
    }
  },
  methods: {
    getCharacters: function(){
      fetch('https://codeclan-guess-who.herokuapp.com/api/characters')
      .then(res=> res.json())
      .then(data=> {
        this.characters = data
        this.mysteryCharacter = data[this.randomInt(data.length)]
      })
    },
    getChoices: function(){
      fetch('https://codeclan-guess-who.herokuapp.com/api/choices')
      .then(res=> res.json())
      .then(data=> this.choices = data[0])
    },
    randomInt: function(max) {
        return Math.floor(Math.random() * Math.floor(max));
    },
    guessCharacter: function(){
      if (this.selectedCharacter.name === this.mysteryCharacter.name){
        this.characterFound = true
      } else {
        this.removeCharacter(this.selectedCharacter)
      }
    },
    removeCharacter: function(character) {
      let index = this.characters.indexOf(character)
      let removed = this.characters.splice(index, 1)
      this.previousSelectedCharacters.push(removed[0])

    }
  },
  components: {
    'list-characters': ListCharacters,
    'select-choices': SelectChoices,
  }
}
</script>

<style lang="css" scoped>
</style>
