<template>
  <div id="tableau">
    <div class="tableauSubstitution">
      <h4>Tableau de substitution</h4>
      <div class="restants" v-if="allChars.length">
        Eléments restants : <span v-for="value in allChars" :key="value">{{ value }} </span>
      </div>
      <div class="row" v-for="(row, i) in tableau" :key="i">
        <input class="value" @input="verifyLetter(i+1, j, $event.target.value, value)" v-model="tableau[i][j]" :class="{ 'header': (i === 0 || j === 0) }" v-for="(value, j) in row" :key="j" :readonly="(i === 0 || j === 0) ? true : false">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TableauSubstitution',
  data () {
    return {
      tableau1: ['-', 'A', 'D', 'F', 'G', 'V', 'X'],
      tableau2: ['A', '', '', '', '', '', ''],
      tableau3: ['D', '', '', '', '', '', ''],
      tableau4: ['F', '', '', '', '', '', ''],
      tableau5: ['G', '', '', '', '', '', ''],
      tableau6: ['V', '', '', '', '', '', ''],
      tableau7: ['X', '', '', '', '', '', ''],
      allChars: ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9']
    }
  },
  methods: {
    randomizeArray: function () {
      for (let i = 2; i <= 7; i++) {
        for (let j = 1; j < this.tableau1.length; j++) {
          let char = this.allChars.splice(Math.floor(Math.random() * (this.allChars.length - 1)), 1)[0]
          // eslint-disable-next-line
          eval('this.tableau' + i)[j] = char
        }
      }
    },
    verifyLetter: function (i, j, newValue, oldValue) {
      if (newValue === '') {
        this.allChars.push(oldValue)
        this.allChars = this.allChars.sort((a, b) => {
          return a[0].charCodeAt(0) - b[0].charCodeAt(0)
        })
      } else if (newValue.length > 1 || this.allChars.find(el => el === newValue) === undefined) {
        // eslint-disable-next-line
        eval('this.tableau' + i)[j] = oldValue
      } else {
        this.allChars.splice(this.allChars.indexOf(newValue), 1)
      }
    }
  },
  filters: {
    onlyOneChar: function (val) {
      return val.charAt(0)
    }
  },
  computed: {
    tableau: function () {
      let tmp = [this.tableau1, this.tableau2, this.tableau3, this.tableau4, this.tableau5, this.tableau6, this.tableau7]
      this.$emit('load', tmp)
      return tmp
    }
  },
  created: function () {
    if (this.tableau2[1] === '') this.randomizeArray()
  }
}
</script>

<style>
h4 {
  text-align: center;
  color: #adff2f;
  font-size: 30px;
}
.row {
  max-width: 80vw;
  margin: 0 auto;
  display: flex;
  flex-flow: row nowrap;
}
.value {
  flex-grow: 1;
  flex-basis: 0;
  text-align: center;
  background: #888;
  padding: 10px 0;
}
.header {
  color: #adff2f;
  font-weight: bolder;
  background: #555;
  border: 0;
}
.restants {
  text-align: center;
  color: white;
  padding: 0 0 20px 0;
}
</style>
