<template>
    <div>
        <div>
          <img v-bind:src="character.image" v-bind:alt="character.name">
          <div>
            <h3>Name: {{character.name}} </h3>
            <button>Ver mas</button>
          </div>
        </div>
    </div>    
</template>


<script>
export default {
   props:['character']
}
</script>