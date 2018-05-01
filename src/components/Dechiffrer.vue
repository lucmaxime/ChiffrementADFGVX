<template>
  <div id="dechiffrer">
    Dechiffrer
    <InputSelect @load="text = $event"/>
    <TableauSubstitution/>
  </div>
</template>

<script>
import TableauSubstitution from './TableauSubstitution'
import InputSelect from './InputSelect'
export default {
  name: 'Dechiffrer',
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
