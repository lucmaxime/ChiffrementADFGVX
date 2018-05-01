<template>
  <div id="inputSelect">
    <div class="label">Saisissez un texte :</div>
    <textarea v-model="formattedText"></textarea>
    <FileReader @load="text = $event"></FileReader>
  </div>
</template>

<script>
import FileReader from './FileReader'

export default {
  name: 'InputSelect',
  data: () => ({ text: '' }),
  computed: {
    formattedText: {
      get: function () {
        let newText = this.text.replace(new RegExp(/[\s]+/, 'g'), ' ').replace(new RegExp(/[^A-Za-z0-9\s]/, 'g'), '')
        this.$emit('load', newText)
        return newText
      },
      set: function (newValue) {
        this.text = newValue
      }
    }
  },
  components: {
    FileReader
  }
}
</script>

<style>
.label {
    display: block;
    text-align: center;
}
.label {
    padding-top: 25px;
    color: #adff2f;
    font-size: 20px;
}
textarea {
    min-width: 80vw;
    max-width: 80vw;
    min-height: 20vh;
    margin: 20px auto;
    display: block;
    background: #666;
    border: none;
    border-radius: 10px;
    padding: 20px;
    font-family: 'Roboto', sans-serif;
    color: #ddd;
    margin-bottom: 30px;
}
</style>
