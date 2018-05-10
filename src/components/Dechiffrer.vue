<template>
  <div id="dechiffrer">
    <InputSelect @load="text = $event.replace(new RegExp(/[\s]/, 'g'), '')"/>
    <Cle @load="key = $event"/>
    <TableauSubstitution @load="tableau = $event"/>
    <div class="midEncodedText">Texte déchiffré intermédiaire :</div>
    <textarea class="noMarginBottom" v-model="midDecodedText" readonly></textarea>
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
      let midDecodedText = this.midDecodedText
      let decodedText = ''
      for (let i = 0; i < midDecodedText.length; i += 2) {
        let char = midDecodedText[i] + '' + midDecodedText[i + 1]
        decodedText += this.flattenTableau.get(char.toUpperCase())
      } 
      return decodedText.toUpperCase()
    },
    midDecodedText: function () {
      if (this.key === '' || this.text === '') return ''

      let keyLength = this.key.length
      let arrayWithKey = []
      let orderedKey = this.key.split('').sort()
      for (let i = 0; i < keyLength; i++) {
        arrayWithKey.push([orderedKey[i]])
      }

      for (let i = 0; i < this.text.length / keyLength; i++) {
        for (let j = 0; j < keyLength % this.text.length; j++) {
          if (Math.floor(this.text.length / keyLength) * i + j < this.text.length) { 
            arrayWithKey[i][j + 1] = this.text[i * Math.floor(this.text.length / keyLength) + j]
          }
        }
      }

      let finalArray = []
      for (let i = 0; i < arrayWithKey.length; i++) {
        finalArray[this.key.indexOf(arrayWithKey[i][0])] = arrayWithKey[i]
      }

      let midDecodedText = ''
      for (let i = 1; i < finalArray[0].length; i++) {
        for (let j = 0; j < finalArray.length; j++) {
          midDecodedText += finalArray[j][i]
        }
      }
      return midDecodedText
    },
    flattenTableau: function () {
      let flatten = new Map()
      for (let i = 1; i < this.tableau.length; i++) {
        for (let j = 1; j < this.tableau[0].length; j++) {
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
