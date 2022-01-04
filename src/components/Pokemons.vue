
<script>
import axios from "axios";
export default {
  name: "Pokemons",
  props: {
    url: String,
    id: Number,
    name: String,
    types: Array
  },
  data () {
    return {
      pokeinfo: {},
      loading: true,
      errored: false
    }
  },

  mounted () {
    axios

        .get(this.url)
        .then(response => (this.pokeinfo = response.data))

        .catch(error => {
          console.log(error)
          this.errored = true
        })

        .finally(() => this.loading = false)

  },
  computed:{

  }

}
</script>
<template>
  <div class="poke-index" >
    <p> Pokemon n°{{pokeinfo.id}}   name : {{pokeinfo.name}}</p><br/>
    <p>types : </p>
    <p v-for="type in pokeinfo.types" :key = "type.id">{{type.type.name}} </p>
  </div>
</template>

<style scoped>

    div{
      border: 1px solid red;
      margin: auto;
      padding: 10px;
      width: 30%;
      display: flex;
      flex-direction: column;
    }
    p{
      margin: 8px;
    }
</style>
