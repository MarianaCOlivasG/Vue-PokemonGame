<template>

  <img 
      class="hidden-pokemon"
      :src="imageSrc" alt="">

  <div class="pokemon-container" >
    <img v-if="showPokemon"
      class="fade-in"
      :src="imageSrc" alt="">
    
    
  </div>

</template>

<script>
export default {
  props: {
    pokemonId: {
      type: Number,
      required: true
    },
    showPokemon: {
      type: Boolean,
      required: true,
      default: false
    }
  },
  computed: {
    imageSrc() {
      return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${ this.pokemonId }.svg`;
    }
  }
}
</script>

<style scope>

.pokemon-container {
    height: 200px;
}

img {
  height: 200px;
  position: absolute;
  width: 100vw;
  margin-left: -50vw;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}

.hidden-pokemon {
    filter: brightness(0);
}
</style>