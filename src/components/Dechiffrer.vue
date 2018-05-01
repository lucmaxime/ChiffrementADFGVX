<template>
  <div id="dechiffrer">
    <InputSelect @load="text = $event"/>
    <Cle @load="key = $event"/>
    <TableauSubstitution @load="tableau = $event"/>
    <div class="encodedText">Texte entièrement déchiffré :</div>
    <textarea class="noMarginBottom" v-model="decodedText" readonly></textarea>
  </div>
</template>

<script>
import TableauSubstitution from './TableauSubstitution'
import InputSelect from './InputSelect'
import Cle from './Cle'
export default {
  name: 'Dechiffrer',
  data () {
    return {
      text: '',
      key: '',
      tableau: []
    }
  },
  computed: {
    decodedText: function () {
      let midEncodedText = ''
      let textWithoutSpaces = this.text.replace(new RegExp(/[\s]+/, 'g'), ' ')
      for (let i = 0; i < textWithoutSpaces.length; i += 2) {
        let char = textWithoutSpaces[i] + '' + textWithoutSpaces[i + 1]
        midEncodedText += this.flattenTableau.get(char.toUpperCase())
      }
      return midEncodedText.toUpperCase()
    },
    flattenTableau: function () {
      let flatten = new Map()
      for (let i = 1; i < this.tableau.length; i++) {
        for (let j = 1; j < this.tableau[i].length; j++) {
          flatten.set(this.tableau[i][0] + this.tableau[0][j], this.tableau[i][j])
        }
      }
      return flatten
    }
  },
  components: {
    TableauSubstitution,
    InputSelect,
    Cle
  }
}
</script>

<style>
</style>
