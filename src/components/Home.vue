<template>
  <div class="home">
    <div class="radios">
      <div @click="toggleRadios('1')" class="radio-dechiffrer">Déchiffrer</div>
      <div @click="toggleRadios('2')" class="radio-chiffrer">Chiffrer</div>
    </div>

    <Chiffrer v-show="isChiffrer"/>
    <Dechiffrer v-show="isDechiffrer"/>
  </div>
</template>

<script>
import Chiffrer from './Chiffrer'
import Dechiffrer from './Dechiffrer'
export default {
  name: 'Home',
  data () {
    return {
      isChiffrer: false,
      isDechiffrer: false
    }
  },
  methods: {
    toggleRadios: (val) => {
      if (!this.isChiffrer && !this.isDechiffrer) {
        this.isDechiffrer = (val === '1')
        this.isChiffrer = (val === '2')
      } else {
        this.isChiffrer = !this.isChiffrer
        this.isDechiffrer = !this.isDechiffrer
      }
    }
  },
  components: {
    Chiffrer,
    Dechiffrer
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.radios {
  margin: 50px auto 0 auto;
  width: 50vw;
  display: flex;
  flex-flow: row nowrap;
  justify-content: space-around;
}
.radios > div {
  flex-basis: 25vw;
  text-align: center;
  padding: 20px 0;
  background: #adff2f;
  transition: all .5s;
}
.radios > div:hover {
  background: #acff2fd0;
  font-size: 1.2em;
  font-weight: bold;
}
.radios div:first-child {
  border-radius: 10px 0 0 10px;
}
.radios div:last-child {
  border-radius: 0 10px 10px 0;
}
</style>
