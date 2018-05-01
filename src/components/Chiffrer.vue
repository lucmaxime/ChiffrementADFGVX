<template>
  <div id="chiffrer">
    <InputSelect @load="text = $event"/>
    <Cle @load="key = $event"/>
    <TableauSubstitution @load="tableau = $event"/>
    <div class="midEncodedText">Texte chiffré intermédiaire :</div>
    <textarea class="noMarginBottom" v-model="midEncodedText" readonly></textarea>
    <div class="encodedText">Texte entièrement chiffré :</div>
    <textarea class="noMarginBottom" v-model="encodedtext" readonly></textarea>
  </div>
</template>

<script>
import TableauSubstitution from './TableauSubstitution'
import InputSelect from './InputSelect'
import Cle from './Cle'
export default {
  name: 'Chiffrer',
  data () {
    return {
      text: '',
      key: '',
      tableau: []
    }
  },
  computed: {
    midEncodedText: function () {
      let midEncodedText = ''
      for (let i = 0; i < this.text.length; i++) {
        let char = this.text[i]
        if (char !== ' ') midEncodedText += this.flattenTableau.get(char.toUpperCase())
      }
      return midEncodedText.toUpperCase()
    },
    flattenTableau: function () {
      let flatten = new Map()
      for (let i = 1; i < this.tableau.length; i++) {
        for (let j = 1; j < this.tableau[i].length; j++) {
          flatten.set(this.tableau[i][j], this.tableau[i][0] + this.tableau[0][j])
        }
      }
      return flatten
    },
    encodedtext: function () {
      if (this.key === '' || this.text === '') return ''

      console.log(this.tableau)

      let keyLength = this.key.length
      let arrayWithKey = []
      for (let i = 0; i < keyLength; i++) {
        arrayWithKey.push([])
        arrayWithKey[i].push(this.key[i])
      }
      for (let i = 0; i < this.midEncodedText.length; i++) {
        let char = this.midEncodedText[i]
        if (char !== ' ') arrayWithKey[i % keyLength].push(char)
      }

      arrayWithKey = arrayWithKey.sort((a, b) => {
        return a[0].charCodeAt(0) - b[0].charCodeAt(0)
      })

      let encodedText = ''
      for (let i = 0; i < arrayWithKey.length; i++) {
        for (let j = 1; j < arrayWithKey[i].length; j++) {
          encodedText += arrayWithKey[i][j]
        }
      }

      return encodedText
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
.midEncodedText {
  text-align: center;
  padding-top: 25px;
  color: #adff2f;
  font-size: 20px;
}
.encodedText {
  text-align: center;
  padding-top: 25px;
  color: #adff2f;
  font-size: 30px;
}
.noMarginBottom {
  margin-bottom: 0;
}
</style>
