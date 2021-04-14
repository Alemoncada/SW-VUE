<template>
  <div>
    <h1>acerca de: {{currentCharacter.name}}</h1>
    <p>Skin color: {{currentCharacter.skin_color}} </p>
    <p>Eye color: {{currentCharacter.eye_color}}</p>
    <p>Genero: {{currentCharacter.gender}}</p>              
  </div>   
</template>

<script>


export default {
  name: 'InfoCharacter',

   data: function(){
    return {
      currentCharacter: [] 
    }
  },    
}  
</script>