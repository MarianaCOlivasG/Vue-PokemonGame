<template>

    <h1 v-if="!pokemon">Cargando...</h1>

    <div v-else>
        <h1>¿Quién es este pokémon?</h1>
    
        <PokemonPicture :pokemonId="pokemon.id" 
                        :showPokemon="showPokemon"/>
        <PokemonOptions 
            :pokemons="pokemonArr"
            @selection-pokemon="checkAnswer( $event )"/>
<!-- selection-pokemon escuchando eventos del componente hijo -->

        <template v-if="showAnswer">
            <h2 class="fade-in">{{ message }}</h2>
            <button @click="newGame">
                Nuevo Juego
            </button>
        </template>

    </div>


</template>

<script>

import PokemonOptions from '@/components/PokemonOptions.vue';
import PokemonPicture from '@/components/PokemonPicture.vue';

import getPokemonOptions from '@/helpers/getPokemonOptions';


export default {
    components: {
        PokemonOptions,
        PokemonPicture
    },
    data() {
        return {
            pokemonArr: [],
            pokemon: null,
            showPokemon: false,
            showAnswer: true,
            message: ''
        }
    },
    methods: {
        async mixPokemonArray() {
            this.pokemonArr = await getPokemonOptions()

            const rndInt = Math.floor( Math.random() * 4 );
            this.pokemon = this.pokemonArr[ rndInt ]

        },
        checkAnswer( selectedId ) {

            this.showPokemon = true;
            this.showAnswer = true;

            selectedId == this.pokemon.id
                ? this.message = `Correcto, ${ this.pokemon.name }`
                : this.message = `Oops, era ${ this.pokemon.name }`
            
        },
        newGame(){
            this.showAnswer = false;
            this.showPokemon = false;
            this.pokemon = null;
            this.pokemonArr = [];

            this.mixPokemonArray();
        }
    },
    /* Cuando el componente "esta montado" Lifecycle */
    mounted(){
        this.mixPokemonArray()
    }
}
</script>
