<template>
<div class="container">
  <div class="text-center">
    <h1>STAR WARS CHARACTERS</h1>
  </div>

  <div >
    <b-row class="justify-content-center" >
      <character @showInfo="showInfo" v-for="character of characters" v-bind:key="character.id" v-bind:character="character" />
    </b-row>  
  </div> 

  <div class="mt-5" >
    <b-row class="justify-content-center">
      <b-button @click="changePage(page-1)" class="m-2">Anterior</b-button>
      <h1> <b-badge>{{page}}</b-badge></h1>
      <b-button @click="changePage(page+1)" class="m-2">Siguiente</b-button>
    </b-row>    
  </div>

      <div>
         <h1>acerca de: {{currentCharacter.name}}</h1>
         <p>Skin color: {{currentCharacter.skin_color}} </p>
         <p>Eye color: {{currentCharacter.eye_color}}</p>
         <p>Genero: {{currentCharacter.gender}}</p>              
      </div>   
       
  </div>
</template>
       

<script>

import axios from 'axios';
import Character from '@/components/Character.vue';

export default {
  name: 'People',
  
  components:{
    Character,
    
  }, 

   data: function(){
    return {
      characters:[],
      page: 1,
      pages: 1,
      currentCharacter: [] 
    }
  },

    created(){
    this.fetch()
  },



  methods:{
    fetch(){
      const params = {
        page: `${this.page}`
      }

      let result =axios.get("https://swapi.dev/api/people/", {params})
      .then((res)=>{
        this.characters = res.data.results;
        this.pages = this.page + 1;
               
      })
    },

    changePage (page){
      this.page = (page <= 0 || page > this.pages) ? this.page : page;
      this.fetch();          
    }, 

    showInfo(url){
      this.fetchOne(url)
    },

    async fetchOne(url){
      let result = await axios.get(url);
      this.currentCharacter = result.data

      console.log(this.currentCharacter, "personaje")
    }
  }  
}  
</script>

