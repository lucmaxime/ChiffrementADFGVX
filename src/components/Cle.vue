<template>
  <div class="cle">
    <input class="input" type="text" value="" placeholder="Choisissez une clé" v-model="keyValueFormatted">
  </div>
</template>

<script>
export default {
  name: 'Cle',
  data () {
    return {
      keyValue: ''
    }
  },
  computed: {
    keyValueFormatted: {
      get: function () {
        let key = this.keyValue.replace(new RegExp(/[^A-Za-z0-9]/, 'g'), '')
        this.$emit('load', key)
        return key
      },
      set: function (newValue) {
        this.keyValue = newValue.toUpperCase()
      }
    }
  }
}
</script>

<style>
.cle {
    margin-top: 30px;
}
.input {
    display: block;
    width: 50vw;
    margin: 0 auto;
    padding: 10px;
    font-family: 'Roboto', sans-serif;
    font-size: 1.5rem;
    text-align: center;
    border-radius: 10px;
    border: 0;
}
</style>
