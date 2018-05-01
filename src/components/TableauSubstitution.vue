<template>
  <div id="tableau">
    Tableau de substitution
    <div class="tableauSubstitution">
      <div v-for="index in 10" :key="index">
        {{ tableau[0][index] }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TableauSubstitution',
  data () {
    return {
      tableau1: ['', 'A', 'D', 'F', 'G', 'V', 'X'],
      tableau2: ['A', '', '', '', '', '', ''],
      tableau3: ['D', '', '', '', '', '', ''],
      tableau4: ['F', '', '', '', '', '', ''],
      tableau5: ['G', '', '', '', '', '', ''],
      tableau6: ['V', '', '', '', '', '', ''],
      tableau7: ['X', '', '', '', '', '', '']
    }
  },
  computed: {
    tableau: function () {
      return [this.tableau1, this.tableau2, this.tableau3, this.tableau4, this.tableau5, this.tableau6, this.tableau7]
    }
  }
}
</script>

<style>
</style>
