<template lang="html">
  <form v-on:submit.prevent="">
    <select v-on:change="whenSelected" v-model='choice1'>
      <option v-for="(choice, index) in choices" v-bind:value="choice" :key="index">{{index}</option>
    </select>
  </form>


</template>

<script>
export default {
  name: 'select-choices',
  props: ['choices'],
  data(){
    choice1: null,
  }
}
</script>

<style lang="css" scoped>
</style>
