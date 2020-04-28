<template lang="html">
  <div>
    <ul v-if="characters" >
      <character-item v-for="character in characters" :character="character"></character-item>
    </ul>
  </div>
</template>

<script>
import CharacterItem from './CharacterItem.vue'

export default {
  name: 'list-characters',
  props: ['characters'],
  components: {
    'character-item': CharacterItem
  }
}
</script>

<style lang="css" scoped>
</style>
