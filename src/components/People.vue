<template>
<div>
  <div>
    <h1>STAR WARS CHARACTERS</h1>
  </div>

  <div>
    <character v-for="character of characters" v-bind:key="character.id" v-bind:character="character" />
  </div>
     
</div>
</template>
  

<script>

import axios from 'axios';
import Character from '@/components/Character.vue';


export default {
  name: 'People',
  components:{
    Character
  },

   data: function(){
    return {
      characters:[],
    }
  },

    created(){
    this.fetch()
  },



  methods:{
    fetch(){
      let result =axios.get("https://swapi.dev/api/people/")
      .then((res)=>{
        this.characters = res.data.results
        console.log(res.data)
      })
    }
  }  
}  
</script>

