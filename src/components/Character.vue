<template>      
  <b-col cols="12" md="4" class="mt-5">
    <b-card-group deck>
      <b-card
        border-variant="danger"
        v-bind:header="character.name"
        header-bg-variant="warning"
        header-text-variant="black lead font-weight-bold font-italic"
        align="center"
      >                           
        <b-list-group flush>
          <b-list-group-item><span class="font-weight-bold text-danger">Height :</span> {{character.height}}</b-list-group-item>
          <b-list-group-item><span class="font-weight-bold text-danger">Mass :</span> {{character.mass}}</b-list-group-item>
          <b-list-group-item ><span class="font-weight-bold text-danger">Homeworld :</span> {{planet}}</b-list-group-item>
        </b-list-group>
        <b-button v-b-modal.modal-scrollable variant="outline-danger" @click="moreInfo(character.url)">More info</b-button>
      </b-card>      
    </b-card-group>
  </b-col>   
       
</template>


<script>

import axios from 'axios';

export default {
    props:['character'],

    data: function(){
    return {
      planet:'',
    }
  },

   created(){
    this.fetch()
  },

  methods:{
    fetch(){        
      let result =axios.get(this.character.homeworld)
      .then((res)=>{
        this.planet = res.data.name;                     
      })
    },

    moreInfo(url){
      this.$emit('showInfo', url)
    }
  }  
}

</script>