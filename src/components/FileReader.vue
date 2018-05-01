<template>
  <div class="file-reader">
    <label for="file" class="label-file">Ou choisissez un fichier texte :</label>
    <input id="file" class="input-file" type="file" @change="loadTextFromFile">
  </div>
</template>

<script>
export default {
  methods: {
    loadTextFromFile (ev) {
      const file = ev.target.files[0]
      const reader = new FileReader()

      reader.onload = e => this.$emit('load', e.target.result)
      reader.readAsText(file)
    }
  }
}
</script>

<style>
.file-reader {
    text-align: center;
}
.label-file {
    display: block;
}
.label-file, .input-file {
    padding-bottom: 15px;
    color: #adff2f;
    font-size: 20px;
}
</style>
