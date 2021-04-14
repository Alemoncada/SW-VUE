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

    <b-modal v-b-modal.modal-xl id="modal-scrollable" scrollable v-bind:title="currentCharacter.name" header-text-variant="lead font-weight-bold font-italic text-danger" >
    <p><span class="font-weight-bold text-dark">Birth year: </span>{{currentCharacter.birth_year}} </p>
    <p><span class="font-weight-bold text-dark">Skin color: </span>{{currentCharacter.skin_color}} </p>
    <p><span class="font-weight-bold text-dark">Eye color: </span>{{currentCharacter.eye_color}}</p>
    <p><span class="font-weight-bold text-dark">Gender: </span>{{currentCharacter.gender}}</p>
    <p><span class="font-weight-bold text-dark"> Films: </span>{{films}}</p>
    <p><span class="font-weight-bold text-dark"> Vehicles: </span>{{this.vehicles ==! [] ? "unknown" : vehicles }}</p>


    </b-modal>


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
      currentCharacter: [],
      films:[],
      vehicles:[],

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
      this.fetchTwo()
      this.fetchThree()
    },

     async fetchTwo(){
      this.films =[]
       for (let film of this.currentCharacter.films){
      let result = await axios.get(film)
      .then((res)=>{
        this.films.push(res.data.title) ;
      })
      }
    },
     async fetchThree(){
      this.vehicles =[];
       for (let vehicle of this.currentCharacter.vehicles){
      let result = await axios.get(vehicle)
      .then((res)=>{
        this.vehicles.push(res.data.name) ;
      })
      }
    },
  }
}
</script>

