<template>
  <div id="chiffrer">
    <InputSelect @load="text = $event"/>
    <Cle @load="key = $event"/>
    <TableauSubstitution/>
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
      key: ''
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
