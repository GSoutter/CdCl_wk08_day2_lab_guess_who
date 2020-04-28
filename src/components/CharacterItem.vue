<template lang="html">
  <div>"
    <li v-on:click="emitCharacter">
      <img src= "/avatars/Alex.png">
      {{character.name}}
    </li>
  </div>
</template>

<script>
import {eventBus} from "../main.js"


export default {
  name: 'character-item',
  props: ['character'],
  methods: {
    emitCharacter: function(){
      eventBus.$emit('character-selected', this.character)
    }
  }

}
</script>

<style lang="css" scoped>
</style>
