<template>
  <div id="chiffrer">
    Chiffrer
    <InputSelect @load="text = $event"/>
    <TableauSubstitution/>
  </div>
</template>

<script>
import TableauSubstitution from './TableauSubstitution'
import InputSelect from './InputSelect'
export default {
  name: 'Chiffrer',
  data () {
    return {
      text: ''
    }
  },
  components: {
    TableauSubstitution,
    InputSelect
  }
}
</script>

<style>
</style>
